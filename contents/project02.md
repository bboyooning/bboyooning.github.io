---
# date: '2022-06-01'
title: '2차 프로젝트 회고'
categories: ['project']
summary: 'wecode 2차 프로젝트 회고'
thumbnail: './project02.png'
---

## [project] 2차 프로젝트 '돌하룻밤' 회고

- 시연영상 : https://www.youtube.com/watch?v=wFNZgmsp6rQ
- 숙박 예약 브랜드 에어비앤비를 모티브로 한 제주도 지역의 단 '하룻밤' 숙박 예약 웹사이트
- 사이트 UI만 참고, 모든 코드 작성은 직접 진행
- 프론트엔드 깃헙 주소 : https://github.com/wecode-bootcamp-korea/31-2nd-DolHaru-frontend
- 백엔드 깃헙 주소 : https://github.com/wecode-bootcamp-korea/31-2nd-DolHaru-backend

### 1. 개발 기간 및 인원

- 개발 기간 : 2022.04.11 - 2022.04.21 (11일)
- 개발 인원 : 6명 ➡️ Front 4명(김민주, 김보윤, 김동욱, 윤서영) / Back 2명(한상안(PM), 김수훈)

### 2. 사용한 기술 스택

- Front-End : React.js, React Router, Styled-Components, Material UI, Kakao 로그인 및 지도 API, React Slick, Date-Picker
- Back-End : Python, Django, AWS(EC2, S3, RDS), MySQL, Kakao dev(login)
- 협업 툴 : Git, Trello, Slack, Notion

### 3. 구현 기능

- Kakao API를 이용한 소셜 로그인 / 회원가입
- 숙소 위치, 특징, 사진 등 전반적인 정보를 등록 가능한 호스팅 기능
- 숙소 전체 리스트 페이지 및 다중 필터링, 페이지네이션 기능
- 숙소 상세페이지 보여주기 기능

### 4. 담당 페이지 및 구현 기능

[담당 페이지]

- 숙소 리스트 페이지

[구현 기능]

- 이미지 슬라이드, 페이지네이션, 다중 필터, Kakao Maps API 여러개 마커 띄우기

### 5. 구현 기능(상세)

- 이미지 슬라이드

  - React Slick Library 를 활용하여 이미지 슬라이드 기능 구현
  - slick 커스터마이징을 통해 구현하고 싶은 UI 에 맞게 수정하여 기능 구현

  ```js
  import styled from 'styled-components'
  import React from 'react'
  import Slider from 'react-slick'
  // css 커스터마이징 파일을 import 시켜준다.
  import 'slick-carousel/slick/slick.css'
  import 'slick-carousel/slick/slick-theme.css'

  const StaylistSlider = ({ images }) => {
    //settings 부분, 슬라이더의 기능을 조정할 수 있다.
    const settings = {
      dots: true,
      infinite: true,
      speed: 500,
      slidesToShow: 1,
      slidesToScroll: 1,
    }
    return (
      <StyledSlide {...settings}>
        //Slider 태그, 위에서 설정한 슬라이더가 나옴
        {images.map((img, index) => (
          <img key={index} src={img} alt="stay slide" />
        ))}
      </StyledSlide>
    )
  }

  export default StaylistSlider

  const StyledSlide = styled(Slider)`
    <!-- 구현하고 싶은 UI 에 맞춰서 진행 -->
  `
  ```

  <br>

- 페이지네이션

  - Staylist 페이지에서 페이지 이동 버튼을 클릭하게 되면 url 이동
  - 이때 url 에는 각 버튼에 해당하는 Query String 이 포함됨
  - 이동한 페이지 url 에 담겨있는 Query String 을 useLocation Hook 을 이용하여 가져옴
  - Query String 에 대한 정보는 useLocation Hook 이 반환한 객체의 search 프로퍼티 안에 담겨있음
  - url 에서 Query String 정보 받아서 이를 통해 데이터를 요청

```js
// Staylist.js
import React, { useEffect, useState, useRef } from 'react'
import { useNavigate, useLocation } from 'react-router-dom'
// ... 중략
import Buttons from './StaylistPagination/Buttons'
import styled from 'styled-components'
import API from './../../config'

const LIMIT = 12 // limit 은 고정값 12, 여러 곳에서 사용하고 있기 때문에 상수 변수로 설정

const Staylist = () => {
  // ... 중략
  const location = useLocation()
  const navigate = useNavigate()
  const [placeList, setPlaceList] = useState([])
  const [offsetNumber, setOffsetNumber] = useState(0)

  useEffect(() => {
    fetch(
      `${API.stays}${
        location.search ? location.search + '&' : '?'
      }limit=${LIMIT}&offset=${offsetNumber}`,
    )
      .then(res => res.json())
      .then(data => setPlaceList(data.stay_list))
  }, [location.search, offsetNumber])

  const updateOffset = ({ buttonIndex }) => {
    setOffsetNumber(buttonIndex * LIMIT)
  }

  // ... 중략

  return (
    <StaylistContainer>
      // ... 중략
      <PageNation>
        <Buttons updateOffset={updateOffset} />
      </PageNation>
    </StaylistContainer>
  )
}

export default Staylist

const StaylistContainer = styled.div`
  overflow-y: scroll;
  scrollbar-width: none;

  &::-webkit-scrollbar {
    display: none;
  }
`
// ... 중략
const PageNation = styled.div`
  width: 53%;
  height: 100px;
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: ${({ theme }) => theme.mainWhite};
`
```

```js
// Button.js
import React from 'react'
import styled from 'styled-components'

const Buttons = ({ updateOffset }) => {
  return (
    <>
      <PageBtn onClick={() => updateOffset(0)}>1</PageBtn>
      <PageBtn onClick={() => updateOffset(1)}>2</PageBtn>
      <PageBtn onClick={() => updateOffset(2)}>3</PageBtn>
      <PageBtn onClick={() => updateOffset(3)}>4</PageBtn>
    </>
  )
}

export default Buttons

const PageBtn = styled.button`
  margin-right: 20px;
  width: 30px;
  height: 30px;
  background-color: ${({ background }) => background};
  color: ${({ color }) => color};
  border: none;
  border-radius: 30px;
  font-size: ${({ theme }) => theme.fontRegular};
`
```

<br>

- 다중 필터
