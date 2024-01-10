# MVC 와 MVVM 패턴의 차이

- MVC(Model-View-Controller) 패턴은 애플리케이션을 모델(Model) , 뷰(View) , 컨트롤러(Controller)로 구분하여 개발하는 방식. 모델은 데이터를 , 뷰는 사용자 인터페이스를 , 컨트롤러는 데이터와 뷰 간의 상호 작용을 관리함.

- MVVM(Model-View-ViewModel) 패턴은 MVC 패턴의 확장으로 , 뷰와 모델 사이에 뷰모델(ViewModel)이 추가된 형태. 뷰모델은 뷰를 표현하기 위한 데이터와 동작을 캡슐화하고 , 뷰와 모델 간의 데이터를 바인딩을 통해 데이터의 변화를 자동으로 반영.