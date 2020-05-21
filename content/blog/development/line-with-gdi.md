---
title: GDI를 사용한 선분 그리기 응용 프로그램
date: 2014-04-11 13:00:00
category: development
thumbnail: './images/direct2-1/computer.jpg'
draft: false
---

GDI를 사용한 Win32 응용프로그램 작성 - 선분 그리기 응용 프로그램


## 1. 처음 실행한 모습
처음 실행한 상태에서 오른쪽 버튼을 클릭하게 되면, `WndProc` 함수에서 WM_RBUTTODWN이 적용이 되고 현재 좌표를 알려준다.

```
LRESULT CALLBACK WndProc(HWND hWnd, UINT message, WPARAM wParam, LPARAM
lParam)
{
  switch (message)
    {
      case WM_RBUTTONDOWN:
        double currentX = LOWORD(lParam);
        double currentY = HIWORD(lParam);
        TRACE(_T("\n오른쪽 마우스 버튼 좌표 = (%d, %d)\n"), (int)currentX, (int)currentY);
```


![처음 실행한 모습 스크린샷](./images/direct2d-1/LineDrawingApplication_1.jpg)
![마우스 좌표 스크린샷](./images/direct2d-1/LineDrawingApplication_2.jpg)

## 2. 메뉴 설명
메뉴는 총 3개의 메뉴가 있다.
![메뉴 모습](./images/direct2d-1/LineDrawingApplication_3.jpg)

파일에서 끝내기를 누르게 되면 현재 돌아가고 있는 프로그램이 종료가 되고 창이 꺼진다.

![메뉴에서 색상을 선택](./images/direct2d-1/LineDrawingApplication_4.jpg)


색상 메뉴를 클릭하게 되면 색을 골를 수 있는 버튼들이 있는 창이 따로 뜨게 된다. 원하는 색을 클릭하고 선택을 누르게 되면 선의 색이 변경이 가능하다. 취소를 누를 경우 색은 변경하지 않고 따로 뜬 색상 고르는 창이 꺼지게 된다.

![색상 선택 창에서 색을 선택](./images/direct2d-1/LineDrawingApplication_5.jpg)

다양한 색상으로 선을 그릴 수 있다.

![다양한 색상의 선 그리기](./images/direct2d-1/LineDrawingApplication_6.jpg)


아래 소스는 색상 메뉴를 클릭했을 때 나오는 창에 대한 소스이다.

```
INT_PTR CALLBACK ColorProc(HWND hDlg, UINT message, WPARAM wParam,
  LPARAM lParam) { //색상 대화 상자의 메시지 처리기
  UNREFERENCED_PARAMETER(lParam);
  switch (message) {
  case WM_INITDIALOG:
    return (INT_PTR) TRUE;
  case WM_COMMAND:
    if (LOWORD(wParam) == IDC_BLACK) {
      selectedColor = 0x000000; // black
      return (INT_PTR) TRUE;
    } else if (LOWORD(wParam) == IDC_RED) {
      selectedColor = 0x0000ff; // red
      return (INT_PTR) TRUE;
    } else if (LOWORD(wParam) == IDC_GREEN) {
      selectedColor = 0x00ff00; // green
      return (INT_PTR) TRUE;
    } else if (LOWORD(wParam) == IDC_BLUE) {
      selectedColor = 0xff0000; // blue
      return (INT_PTR) TRUE;
    } else if (LOWORD(wParam) == IDOK) {
      // 현재 컬러를 갱신
      currentColor = selectedColor;
      EndDialog(hDlg, LOWORD(wParam));
      return (INT_PTR) TRUE;
    } else if (LOWORD(wParam) == IDCANCEL) {
      // 취소
      EndDialog(hDlg, LOWORD(wParam));
      return (INT_PTR) TRUE;
    }
    break;
  }
  return (INT_PTR) FALSE;
}
```

메뉴의 마지막으로 도움말의 정보를 누르게 되면 프로그램에 관한 정보를 볼 수 있다.

![메뉴에서 도움말 메뉴](./images/direct2d-1/LineDrawingApplication_7.jpg)

![도움말 메뉴를 클릭하면 나오는 정보 메뉴](./images/direct2d-1/LineDrawingApplication_8.jpg)

![프로그램 정보](./images/direct2d-1/LineDrawingApplication_9.jpg)

