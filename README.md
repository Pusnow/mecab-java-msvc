# mecab-java-msvc

[![Build status](https://ci.appveyor.com/api/projects/status/bxtc772o72obpkvb/branch/master?svg=true)](https://ci.appveyor.com/project/Pusnow/mecab-java-msvc/branch/master)

mecab-java-msvc는 mecab-ko-msvc에서 사용할 수 있는 mecab-java을 빌드하는 프로젝트입니다.

## 설치

* [mecab-ko-msvc](https://github.com/Pusnow/mecab-ko-msvc/)를 설치하지 않았으면 설치해야 합니다.
* [mecab-ko-dic-msvc](https://github.com/Pusnow/mecab-ko-dic-msvc/)를 설치하지 않았으면 설치해야 합니다.
* 실행 환경에 맞는 [최신버전](https://github.com/Pusnow/mecab-java-msvc/releases/latest)을 다운로드합니다. JDK 1.8을 지원합니다.

## 사용 정보
* `org` 폴더와 `MeCab.dll`이 있는 경로에서 Java 파일을 편집합니다.
* 첨부한 `test.java`는 UTF-8로 인코딩 되어 있습니다. `javac -encoding UTF-8 test.java` 처럼 인코딩을 지정해 주어야 합니다.
* `java test` 로 테스트 파일을 실행할 수 있습니다.


## 빌드 정보

* mecab-java-msvc 는 [Appveyor](https://www.appveyor.com)를 이용합니다.
* 빌드 과정은 [Appveyor 페이지](https://ci.appveyor.com/project/Pusnow/mecab-java-msvc) 에 기록되어 있습니다.
* 개인적으로 빌드를 하고 싶으신 분은 [appveyor.yml](https://github.com/Pusnow/mecab-java-msvc/blob/master/appveyor.yml) 을 참고하시기 바랍니다.



[mecab-java](https://code.google.com/p/mecab/downloads/detail?name=mecab-java-0.996.tar.gz&can=2&q=) 의 tagger와 lexicon의 메모리 누수가 해결된 버전

MeCab java module

$Id: README,v 1.2 2005/12/25 16:55:43 taku-ku Exp $;

1. Build UTF-8 dictionary

2. How to use?

  See test.java as sample program.

  % java -classpath MeCab.jar test -d ../dic