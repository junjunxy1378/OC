## 웹사이트를 개발하고자 한다.

## 자료
/Users/jun/claude-project/OC/OC.xlsx 는 overlap cloner라는 plasmid를 assembly 하는 도구를 계산하기 위한 excel이다.

## Frag#2의 계산 흐름
1. assembly는 이으려는 fragment의 수에 따라서, sheet를 선택한다.
2. 긴 DNA의 길이와 양을 입력한다.(B2, B3)
3. 짧은 DNA의 양을 입력한다. (B6)
4. 긴 DNA의 pmol과 1:1이 되는 짧은 DNA의 양을 출력한다. (B7)
5. B3과 B7 값의 합을 보여준다. (이때 출력값이 300이상이면, 빨간색으로 경고한다)
6. 내가 가지고 있는 DNA의 양을 입력한다. (D3, D7)
7. 반응에 사용하는 DNA의 양을 출력한다. (E3, E7)
8. OC 반응이 10인 경우, Enzyme과 10X buffer를 각각 1사용하고, E3과 E7의 합을 사용하고, 남는 용액은 DW의 값으로 출력한다.

## 방향
이러한 계산을 하는 웹사이트를 핸드폰에서 보기 좋은 방식으로 만들고 싶다.
