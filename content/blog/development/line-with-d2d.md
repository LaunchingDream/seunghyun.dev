---
title: D2D를 사용한 선분 그리기 응용프로그램 작성
date: 2014-04-06 13:00:00
category: development
thumbnail: './images/direct2-1/computer.jpg'
draft: false
---

## 1. 처음 실행한 모습

![처음 실행한 모습 스크린샷](./images/line-with-d2d/Create_line_Drawing_Application_usingD2D_report_1.jpg)

소스를 실행한 처음 모습이다. 창에 프로그램 이름을 확인 할 수 있고 축소, 확대, 끄기 버튼이 생성되어 있다.

```C
// 초기화 함수
// 윈도우 application 생성
HRESULT Draw::Initialize(HINSTANCE hInstance) {
    HRESULT hr;
    // D2D 장치 비의존적(독립적) 자원을 생성, 초기화
    hr = CreateDeviceIndependentResources();
    if (SUCCEEDED(hr)) {
      WNDCLASSEX wcex = {
        sizeof(WNDCLASSEX)
      };
      wcex.style = CS_HREDRAW | CS_VREDRAW;
      wcex.lpfnWndProc = Draw::WndProc;
      wcex.cbClsExtra = 0;
      wcex.cbWndExtra = sizeof(LONG_PTR);
      wcex.hInstance = hInstance;
      wcex.hbrBackground = NULL;
      wcex.lpszMenuName = MAKEINTRESOURCE(IDC_WINAPP);
      wcex.hCursor = LoadCursor(NULL, IDI_APPLICATION);
      wcex.lpszClassName = L "D2DDraw";
      RegisterClassEx( & wcex); // 윈도우 클래스를 등록함
      // Create the window
      hwnd = CreateWindow(
        L "D2DDraw", L "HW#3: D2D_ 201001046(유승현)",
        WS_OVERLAPPEDWINDOW, CW_USEDEFAULT,
        CW_USEDEFAULT,
        640, 480, NULL, NULL, hInstance, this
      );
      hr = hwnd ? S_OK : E_FAIL;
      if (SUCCEEDED(hr)) {
        ShowWindow(hwnd, SW_SHOWNORMAL);
        UpdateWindow(hwnd);
      }
    }
    return hr;
```
초기화 함수에 해당하는 소스이다. 사실 완벽하게 이해가 안되지만, D2D 자원들을 초기화 해주고 창을 띄어주는 기능을 한다.

![오른쪽 마우스 버튼 좌표를 출력](./images/line-with-d2d/Create_line_Drawing_Application_usingD2D_report_2.jpg)

```C
// 현재 마우스 클릭한 위치의 X를 currentX, Y를 currentY 변수에 저장
double currentX = LOWORD(lParam);
double currentY = HIWORD(lParam);
// 오른쪽 마우스 클릭 좌표 표시
// 좌표 출력은 디버깅 모드에서 가능
TRACE(_T("\n오른쪽 마우스 버튼 좌표 = (%d, %d)\n"),
  (int) currentX, (int) currentY);
```

처음 실행한 상태에서 오른쪽 버튼을 클릭하게 되면, WM_RBUTTODWN이 적용이 된다. 선분이 하나도 없을 경우 단순히 현재 좌표만을 알려준다.