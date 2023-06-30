0. 설명
bin-실행화일들
***용량을 줄이기 위해 ubuntu용 실행화일등록부에 있는 datas등록부는 windows것과 같으므로 빈 등록부로 두었다.
source-원천
	windows-visual studio 2019
	ubuntu-qtcreator
windows용 원천을 콤파일하려면???
먼저 opencv4.5.3과 opencv-contrib4.5.3을 static으로 콤파일하여 생기는 .lib화일들을 OpenCVx86/lib등록부안에 넣어야 한다.
ubuntu용 원천을 콤파일하려면???
먼저 opencv4.5.3과 opencv-contrib4.5.3을 CMake를 리용하여 static으로 콤파일하고 install하여야 한다.

1. FaceMagicPC.exe
두개의 얼굴화상에 대하여 류사도를 평가하는 프로그람이다.

입구파라메터에 따라 봉사기 또는 단독프로그람으로 실행한다.

1) 봉사기
봉사기로 실행시키려면 파라메터가 없이 또는 포구번호만을 가지고 실행시킨다.
파라메터없이 실행하면 봉사기로 기동하며 이때 포구번호는 12102이다.

실행실례
FaceMagicPC.exe
또는
FaceMagicPC.exe 8899(...포구번호...)

2) 단독프로그람
-i : 입구화상경로
-a : 추가정보
-c : 비교방식(주지 않으면 생활사진비교방식으로 비교한다)

(1) 입구화상경로
절대경로 또는 상대경로로 줄수 있다.
실례: -i F:\img\1.jpg
(2) 추가정보
o 얼굴만 있는 화상

10:10:30:30형식 얼굴령역정보(Left:Top:Right:Bottom형식--공백을 포함하지 않는다)

실례
-a o
-a 10:20:90:100

(3) 비교방식
0 : 생활사진
1 : ID카드

실례
-c 0

단독실행을 위한 실례1:
FaceMagicPC.exe -i F:\img\1.jpg -i F:\img\2.jpg -a o -c 1
우의 실례는 1.jpg에서는 얼굴을 찾아서 쓰고 2.jpg는 얼굴만 있는 화상이므로 그대로 얼굴로 쓰며 비교방식은 ID카드방식으로 한다는것이다.

단독실행을 위한 실례2:
FaceMagicPC.exe -i F:\img\1.jpg -a o -i F:\img\2.jpg -a 10:30:140:200
우의 실례는 1.jpg는 얼굴만 있는 화상이고 2.jpg는 left=10,top=30,right=140,bottom=200령역안에 얼굴이 있으므로 얼굴찾기는 하지 말고 특징비교만을 진행하라는것이며 이때 비교방식은 생활사진방식(주지 않았으므로 기정값을 사용)이다.

(4) 실행결과

형식: json

{
	"overall" : 0,
	"value" : 0.95
}

overall: 결과형식
0: 정상결과
1: 첫 화상에서 얼굴검색실패
2: 두번째 화상에서 얼굴검색실패
3: 첫 화상의 믿음도오유
4: 두번째 화상의 믿음도오유

2. FaceMagicLauncher.exe
FaceMagicPC.exe가 봉사기형식으로 기동했을때 의뢰기로서 동작하는 프로그람이다.

-ip : 봉사기IP주소(주지 않으면 127.0.0.1로 한다.)
-p : 봉사기포구번호(주지 않으면 12102로 한다.)
-i : 입구화상경로
-a : 추가정보
-c : 비교방식(주지 않으면 생활사진비교방식으로 비교한다)

실행실례
FaceMagicLauncher.exe -ip 10.10.20.128 -p 8899 -i F:\img\1.jpg -i F:\img\2.jpg -a o -c 1

실행결과는 단독프로그람에서의 실행결과와 같다.
