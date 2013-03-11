# Ember.js Docs 한국어역

## 개요

### Ember.js는

Ember.js은 대규모 웹 애플리케이션을 구축하는 표준 애플리케이션 구조를 제공하며 boilerplate code 를 배제한 JavaScript 프레임워크.

#### boilerplate code 의 배제

모든 웹 애플리케이션, 예를들어, 데이터를 서버에서 검색하여 화면에 표시하고 데이터에 변경이있는 경우에 표시를 업데이트하는 등 공통작업이 존재한다.

브라우저 측이 준비한 도구는 아주 원시적인 탓에 이러한 작업을 수행하는데 동일한 코드를 여러 번 작성하게 된다. Ember.js는 그 수백 번이나 쓴 적이있는듯한 똑같은 코드를 쓰는 대신에 애플리케이션 그 자체에 집중할 수 있는 도구를 제공하고 있다.

여러 애플리케이션을 만들어 온 경험에서 명백한 저레벨의 이벤트 기반의 추상화는 물론, 전체 애플리케이션, 특히 DOM 그 자체에 이벤트를 전달하는데 필요한 boilerplate code 를 제거하고 있다.

간단한 예로`Person`템플릿을 보기 바란다.

  {{person.name}} is {{person.age}}.

어떤 템플릿 시스템에서도 템플릿이 초기에 렌더링되면 현재의 `Person`의 상태를 반영한다. boilerplate code를 피하기 위해 Ember.js에서는 `Person`의 `name` 또는 `age`의 데이터를 변경하는 동시에 DOM도 자동으로 업데이트 된다.

템플릿을 한 번 지정하면 Ember.js는 템플릿이 항상 업데이트 되도록 하고 있다.

#### 애플리케이션 구조의 제공

웹 애플리케이션이 정적 문서에 지나지 않는 웹페이지에서 진화했기 때문에 브라우저는 충분한 토대를 마련하고 있지 않다.

Ember.js 는 애플리케이션을 Model, View, Controller로 쉽게 분할 할 수있다. 이 패턴은 테스트 용이성을 향상시키고 코드의 모듈성을 강화하며 프로젝트에 참여하기 시작한지 얼마 안된 개발자가 프로젝트에서 어떻게 전체의 JavaScript 소스가 작성되어 있는지 이해를 돕는다. 콜백에 의한 스파게티 코드의 시대는 끝난것이다.

### Ember.js의 특징

기존의 웹 애플리케이션에서는 사용자에게 서버와 통신을 할 때마다 항상 새로운 페이지를 다운로드하게 한다. 즉 통신에서 애플리케이션(서버)과 사용자 사이의 지연시간 이상의 속도를 낼 수는 없다. AJAX를 활용하여 페이지 중 몇몇 파트만을 교체하는 방법은 어느 정도는 도움이 된다. 하지만 UI 업데이트를 하기 위해서는 서버와의 연결 라운드 트립은 피할 수 없다. 그리고 페이지의 여러 파트를 동시에 업데이트 할 필요가 있는 경우에 대부분의 개발자는 모든 요소를 동기화하는 것은 처리하기 어렵기 때문에 페이지를 리로드 하는것에 의지하게 된다.

Ember.js는 다른 모던 JavaScript 프레임워크와 마찬가지로 약간 다른 구현을 하고있다. 많은 애플리케이션의 로직을 서버에 두는 것과 달리, Ember.js 애플리케이션은 작동하는데 필요한 모든 것을 초기 페이지로드시에 다운로드한다. 즉 사용자가 애플리케이션을 사용하는 경우, 사용자는 새로운 페이지를 로드 할 필요도 없고 사용자의 상호 작용에 의한 UI의 반응 속도가 매우 빠르다.

이 구조의 장점 중 하나는 서버 측에 크게 의존하는 어플리케이션이나 다른 사람이 사용하는 REST API를 처리 할 수있는 것이다. 이렇게 함으로써 back-end 개발자는 안전하고 신뢰할 수있는 빠른 API 서버 구축에 집중 가능하고 front-end 개발자가 전문가일 필요도 없다.

### Ember.js를 간단히 소개

Ember를 즐겁게 사용할 수있는 3가지 특징은 :

- 바인딩(Binding)
- 계산된 속성 (Computed properties)
- 자동으로 업데이트하는 템플릿

#### 바인딩

바인딩을 사용하여 두 개의 서로 다른 객체의 속성을 동기화 할 수있다. 바인딩을 한 번 정의하면 Ember 가 변경을 양방향으로 전달하게 한다.

다음이 두 객체 간의 바인딩을 생성하는 방법이다.

	MyApp.president = Ember.Object.create({
		name: "Barack Obama"
	});
	MyApp.country = Ember.Object.create({
		// 'Binding'라는 문자열을 속성 이름의 마지막에 부여하면
		// Ember는`presidentName`속성에 바인딩을 수행
		presidentNameBinding: 'MyApp.president.name'
	});
	// 이후 Ember가 바인딩을 한 후 ...
	MyApp.country.get('presidentName');
	// 결과: "Barack Obama"

바인딩은 애플리케이션을 MVC (Model-View-Controller) 패턴을 사용하여 설계하는 것을 가능하게하여 데이터가 항상 계층 간에 정확히 순환하는 안정성을 얻을 수있다.

#### 계산된 속성 (Computed properties)

계산된 속성(Computed properties)은 함수을 속성처럼 다룰 수 있다 :

	MyApp.president = Ember.Object.create({
		firstName: "Barack",
		lastName: "Obama",
		fullName: function() {
			return this.get('firstName') + ' ' + this.get('lastName');
			// 다음과 같은 방식으로 함수를 속성으로 취급 할 수있다
		}.property()
	});
	MyApp.president.get('fullName');
	// 결과: "Barack Obama"

계산된 속성 (Computed properties)이 유용한 이유는 다른 속성과 마찬가지로 바인딩을 사용할 수 있다는 점이다.

계산된 속성 (Computed properties)은 다른 속성에 의존하는 경우가 많다, 예를들어 위의 예에서 `fullName`속성은 `firstName`와 `lastName`에 의해 값을 확정 할 수있다. Ember에서는 이러한 종속성을 다음과 같이 설정할 수 있다 :

	MyApp.president = Ember.Object.create({
		firstName: "Barack",
		lastName: "Obama",
		fullName: function() {
    	return this.get('firstName') + ' ' + this.get('lastName');
			// Ember 에 대해 이 계산된 속성 (Computed properties)이
			// firstName과 lastName에 종속성이 있는 설정을 수행
		}.property('firstName', 'lastName')
	});

계산된 속성 (Computed properties) 과 관련된 바인딩을 업데이트 할 때 Ember 가 이러한 의존에 대해서도 해결하도록 의존 관계 설정을 제대로해 둘것.

#### 자동으로 업데이트하는 템플릿

Ember는 Handlebar, 시맨틱 템플릿 라이브러리를 이용하고있다. JavaScript 애플리케이션에서 데이터를 검색하여 DOM에 삽입하려면`<script>`태그를 HTML내의 표시 할 위치에 작성하면 된다 :

	<script type="text/x-handlebars">
		The President of the United States is {{MyApp.president.fullName}}.
	</script>

템플릿 또한 바인딩의 대상이 되고있는 점이 가장 장점이다. 무슨 뜻인가하면, 표시할 속성 값을 변경하면 자동으로 표시를 업데이트하는 것이다. 그리고 의존 관계를 명확하게하고 있으면, 의존하는 속성 값을 변경해도 표시 업데이트가 진행된다.

이 세 가지 강력한 도구가 어떻게 작동하는지 알 수 있었는가? 우선 간단한 속성부터 시작하고 그것에서 좀 더 정교한 속성을 설정하여 계산된 속성 (Computed properties)을 사용하여 의존 관계을 명확히 해 나간다. 데이터가 어떠한 것인지 알기만 하면 어떻게 표시할지 여부를 설정하는 것은 한 번만 하고, 나머지는 Ember가 해결할 수 있다. 데이터를 XHR 요청으로부터 취득하던지, 또는 사용자 액션에 의한 것이든지, UI는 항상 최신 상태를 유지할 수 있다. 이는 개발자가 매일 머리를 싸메고 있는 여러가지 종류의 엣지 케이스를 제거 할 수 있다.

## 바로 사용해 보자

요구에 따른 여러가지 최초의 Ember.js 어플리 작성방법이 있다.

만약 요구가 단순하거나 혹은 단지 Ember.js를 사용해보고 싶은 것 뿐이라면, Ember.js의 스타터 키트를 다운로드하기 바란다.
스타터 키트는 [HTML5 Boilerplate (http://html5boilerplate.com/)를 기반으로 하고 있다. 빌드 도구 및 기타 도구는 필요 없다. 스타터 키트를 다운로드하고 압축해제하는 것만으로 된다. Handlebars 템플릿을 편집 할 경우`index.html`에서 하고 Ember.js 어플 자체는`javascripts/app.js`에 들어있다.

보다 큰 애플리케이션의 경우는 Ruby on Rails의 이용을 고려하기 바란다. Rails는 소스 ​​코드 및 기타 asset을 관리하는 데 도움을 줄 뿐만 아니라 REST API도 제공하고 있다.

## Ember Object 모델

Ember 는 단순한 JavaScript 의 객체 모델을 확장하여 바인딩과 옵저버를 추가한다. 뿐만 아니라 더 강력한 믹스 인을 이용한 접근코드 공유도 지원한다.

가장 간단한 예로 `Ember.Object`에서 `extend`메서드를 사용해 Ember 클래스를 만들 수 있다.

	Person = Ember.Object.extend({
		say: function(thing) {
			alert(thing);
		}
	});

새로운 클래스를 만들었으면`create`메서드를 사용하여 새로운 인스턴스를 생성 할 수있다. 클래스에서 설정한 속성 모두를 인스턴스에서 사용할 수있다.

	var person = Person.create();
	person.say("Hello") // alerts "Hello"

인스턴스를 생성할때 속성을 객체에 전달하여 추가할 수있다.

	var tom = Person.create({
		name: "Tom Dale",
		helloWorld: function() {
		this.say("Hi my name is " + this.get('name'));
		}
	});
	tom.helloWorld() // alerts "Hi my name is Tom Dale"

Ember는 바인딩과 옵저버를 지원하고 있기 때문에, `get`메서드를 사용해 언제든지 속성을 가져올 수 있고, `set`메서드를 사용하여 속성설정도 가능하다.

객체에 대해 새로운 인스턴스를 생성 할 때 클래스에서 설정한 메서드 또는 속성을 재정의 할 수도 있다. 예를들어 다음 예제에서는 `Person`클래스의 `say`메서드를 재정의하고 있다.

	var yehuda = Person.create({
		name: "Yehuda Katz",
		say: function(thing) {
			var name = this.get('name');
			this._super(name + " says: " + thing);
		}
	});

객체내에서 `_super`메서드 (`super`는 JavaScript 예약어)를 사용하여 재정의한 원래 메서드를 호출 할 수도 있다.

### 클래스, 서브 클래스

클래스에서 서브 클래스를 작성하는데도 `extend`메서드를 사용할 수있다. 어쨌든 위의 예에서도`extend`메서드를`Ember.Object`에서 이용한 경우에도 실은 `Ember.Object`의 서브 클래스를 작성하고 있던것이 된다.

	var LoudPerson = Person.extend({
		say: function(thing) {
			this._super(thing.toUpperCase());
		}
	});

서브 클래스를 생성 할 때 `this._super`를 사용하여 재정의한 메서드를 수행 할 수있다.

### 클래스와 인스턴스의 재개

클래스는 한번에 모두 정의할 필요는 없고, `reopen`메서드를 사용해 언제든지 클래스를 다시 열어 새로운 속성을 설정할 수 있다.

	Person.reopen({
		isPerson: true
	});
	Person.create().get('isPerson') // true

`reopen`메서드에서는 `this._super`를 이용할 수도 있고, 기존의 방법을 재정의 할 수도 있다.

	Person.reopen({
		// `say`메서드를 !를 마지막에 추가하여 재정의 한다
		say: function(thing) {
			this._super(thing + "!");
		}
	});

예에서와 같이 `reopen`은 인스턴스에 대해 메서드와 속성을 추가하는데 사용하고있다. 클래스의 메서드를 만들고 싶거나 클래스 그 자체에 속성을 추가하려면 `reopenClass`를 이용할 수 있다.

	Person.reopenClass({
		createMan: function() {
			return Person.create({isMan: true})
		}
	});
	Person.createMan().get('isMan') // true

### 계산된 속성 Getters

대부분의 경우 어떤 속성을 다른 속성의 결과를 바탕으로 생성하고 싶은 경우가 있다. Ember 의 객체 모델에서는 일반적인 클래스 설정내에서 계산된 속성을 쉽게 설정할 수 있다.

	Person = Ember.Object.extend({
		// these will be supplied by `create`
		firstName: null,
		lastName: null,
		fullName: function() {
			var firstName = this.get('firstName');
			var lastName = this.get('lastName');
			return firstName + ' ' + lastName;
		}.property('firstName', 'lastName')
	});
	var tom = Person.create({
		firstName: "Tom",
		lastName: "Dale"
	});
	tom.get('fullName') // "Tom Dale"

Ember 의 prototype 확장을 사용하지 않는 경우에도 함수를`Ember.computed`로 묶어 약간 중복된 방법으로도 설정가능하다.

	Person = Ember.Object.extend({
		// these will be supplied by `create`
		firstName: null,
		lastName: null,
		fullName: Ember.computed(function() {
			var firstName = this.get('firstName');
			var lastName = this.get('lastName');
			return firstName + ' ' + lastName;
		}).property('firstName', 'lastName')
	});

`property`메서드는 함수를 계산된 속성 (Computed properties)으로 정의할 뿐만 아니라 종속 관계도 정의한다.

이러한 의존 관계는 이후 바인딩과 옵저버의 설명을 할 때 다시 나온다.

클래스 내에서 서브 클래스를 설정하거나 새로운 인스턴스를 생성하는 경우에, 모든 계산된 속성 (Computed properties)은 재정의 할 수 있다.

### 계산된 속성 Setters

계산된 속성 (Computed properties)을 세트 할 때 Ember가 무엇을해야 할지도 정의할 수있다. 계산된 속성 (Computed properties)을 설정할 때 설정하려는 키 값과 함께 실행하는 것이 가능하다.

	Person = Ember.Object.extend({
		// these will be supplied by `create`
		firstName: null,
		lastName: null,
		fullName: Ember.computed(function(key, value) {
			// getter
			if (arguments.length === 1) {
				var firstName = this.get('firstName');
				var lastName = this.get('lastName');
				return firstName + ' ' + lastName;
				// setter
			} else {
				var name = value.split(" ");
				this.set('firstName', name[0]);
				this.set('lastName', name[1]);
				return value;
			}
		}).property('firstName', 'lastName')
	});
	var person = Person.create();
	person.set('fullName', "Peter Wagenet");
	person.get('firstName') // Peter
	person.get('lastName') // Wagenet

Ember는 계산된 속성 (Computed properties)을 setter에서도 getter에서도 호출 할 수 있으며, 매개 변수의 갯수에 의해 setter로 호출되었는지, getter로 호출되었는지를 확인 할 수있다.

### 옵저버

Ember는 어떤 속성에서도, 물론 계산된 속성 (Computed properties)에도 옵저버를 설정할 수있다. `addObserver`메서드를 사용해 옵저버를 설정한다.

	Person = Ember.Object.extend({
		// these will be supplied by `create`
		firstName: null,
		lastName: null,
		fullName: Ember.computed(function() {
			var firstName = this.get('firstName');
			var lastName = this.get('lastName');
			return firstName + ' ' + lastName;
		}).property('firstName', 'lastName')
	});
	var person = Person.create({
		firstName: "Yehuda",
		lastName: "Katz"
	});
	person.addObserver('fullName', function() {
		// deal with the change
	});
	person.set('firstName', "Brohuda"); // observer will fire

계산된 속성 (Computed properties)인 `fullName`은 `firstName`에 의존하고 있기 때문에, `firstName`이 업데이트되면 `fullName`의 옵저버도 실행된다.

옵저버는 매우 일반적이기 때문에 Ember에서는 클래스내에서 옵저버를 설정하는 방법도 제공하고 있다.

	Person.reopen({
		fullNameChanged: function() {
			// .addObserver 인라인 버전
		}.observes('fullName')
	});

prototype 확장을 사용하지 않는 경우에도 `Ember.observer`메서드를 사용하여 인라인 옵저버의 설정이 가능하게된다.

	Person.reopen({
		fullNameChanged: Ember.observer(function() {
		//  .addObserver 인라인 버전
		}, 'fullName')
	});

#### 배열 내의 변경

계산된 속성 (Computed properties)을 배열내의 모든 요소에 의존하는 형태로 설정하는 경우도 많다. 예를들어 컨트롤러에있는 모든 TODO 항목 수를 세어 그 안에 몇개가 완료 상태를 가지고 있는지를 계산하고 싶은 경우 등이 거기에 해당한다.

아래가 그 경우의 계산된 속성 (Computed properties)의 예 :

	App.todosController = Ember.Object.create({
		todos: [
		Ember.Object.create({
			isDone: false
		})],
		remaining: function() {
			var todos = this.get('todos');
			return todos.filterProperty('isDone', false).get('length');
		}.property('todos.@each.isDone')
	});

`@each`라는 특별한 키가 의존 관계내의 (`todos@each.isDone`)에 있음을 주목하기 바란다. 이렇게 하는것으로 Ember.js 에 대해 다음 4 가지의 이벤트에서 바인딩 업데이트 및 이 계산된 속성 (Computed properties)의 옵저버를 실행하도록 지시 할 수있다.

- `todos`배열의 객체에서`isDone`속성 변경
- `todos`배열에 항목 추가
- `todos`배열에서 항목 삭제
- 컨트롤러내의`todos`속성이 다른 배열로 변경

위의 예에서 `remianing`은 `1`이된다 :

	App.todosController.get('remaining');
	// 1

todo내의`isDone`속성을 변경하면`remianing`속성은 자동으로 업데이트된다 :

	var todos = App.todosController.get('todos');
	var todo = todos.objectAt(1);
	todo.set('isDone', true);
	App.todosController.get('remaining');
	// 0
	todo = Ember.Object.create({ isDone: false });
	todos.pushObject(todo);
	App.todosController.get('remaining');
	// 1

### 바인딩

바인딩은 두 가지 속성 간에 링크를 형성한다. 어느 한쪽이 새 값으로 업데이트되면 다른 한쪽도 자동으로 업데이트된다. 바인딩은 같은 객체의 속성을 링크 할 수도 있으며, 다른 객체 사이에서도 링크 가능하다. 바인딩을 구현하는 다른 프레임워크와는 달리 Ember.js 의 바인딩은 view와 model 사이의 객체뿐만 아니라 어떤 객체도 이용할 수있다.

2-way 바인딩을 만드는 가장 손쉬운 방법은 새로운 속성에 `Binding`라는 문자열을 마지막에 추가하여 글로벌 스코프로부터의 경로를 지정하는 방법이다 :

	App.wife = Ember.Object.create({
		householdIncome: 80000
	});
	App.husband = Ember.Object.create({
		householdIncomeBinding: 'App.wife.householdIncome'
	});
	App.husband.get('householdIncome'); // 80000
	// Someone gets raise.
	App.husband.set('householdIncome', 90000);
	App.wife.get('householdIncome'); // 90000

바인딩은 즉시 업데이트하지 않는 것에 주의하길 바란다. Ember에서는 애플리케이션의 코드가 모두 실행될 때까지 동기를 기다린다. 이렇게 함으로써 바인딩 된 속성을 여러 번 변경해도 값이 일회성이라도 동기에 소요되는 낭비를 배제하는 걱정이 없어진다.

#### 1-way 바인딩

1-way 바인딩은 변경을 한 방향으로만 전달하게 한다. 일반적으로는 한 방향 바인딩은 성능 최적화에 사용되어 2-way 바인딩의 구문을 좀 더 간결하게 할 수있다.

	App.user = Ember.Object.create({
		fullName: "Kara Gates"
	});
	App.userView = Ember.View.create({
		userNameBinding: Ember.Binding.oneWay('App.user.fullName')
	});
	// user 객체내의 name 변경은
	// view내의 값을 변경한다.
	App.user.set('fullName', "Krang Gates");
	// App.userView.userName은 "Krang Gates"로 변경
	// ... 그러나 View의 변경은 오브젝트에 반영되지 않는다
	App.userView.set('userName', "Truckasaurus Gates");
	App.user.get('fullName'); // "Krang Gates"

### 무엇을 언제 사용하면 좋을까?

익숙해지기 전에는 계산된 속성 (Computed properties)과 바인딩, 그리고 옵저버를 언제 사용해야 할지 모르는 경우도있다. 그 경우 다음 지침을 참조해 주었으면한다 :

− 계산된 속성 (Computed properties)은 다른 속성을 사용하여 새로운 속성을 혼합하는데 이용한다. 계산된 속성 (Computed properties)은 애플리케이션의 동작을 포함해야 하는것이 아니라 일반적으로 호출될 때 부작용을 유발해서는 안된다. 그러나 드문 경우로, 여러 번에 걸쳐 같은 계산된 속성 (Computed properties)의 호출은 항상 같은 값을 반환해야한다 (물론 의존하는 속성에 변경이 없으면)

- 옵저버는 다른 속성의 변경에 반응하는 동작을 정의 해야한다. 옵저버는 특히 바인딩의 동기가 끝난 때 어떤 동작을 할 때 아주 효과적.

- 바인딩은 객체가 서로 다른 두 개의 레이어가 항상 동기화 상태인것을 확인하기 위해 자주 사용된다. 예를들어, 컨트롤러에 대해 Handlebars를 통해 View 를 바인딩하는 등. 물론 두 객체를 동일한 레이어내에서 동기화하기 위하여 사용할 수있다. 예를들어 `App.selectedContactController`가 `App.contactsController`의 `selectedContact`에 바인딩하는 등의 경우가 그렇다.

## 네임 스페이스 작성

모든 Ember 어플리케이션은 `Ember.Application`인스턴스가 있어야한다. 이 객체는 전역으로 액세스 할 수있는 네임 스페이스로서의 역할을하고 어플리케이션 내 다른 클래스나 인스턴스로부터 액세스 할 수있다. 또한 페이지에 대해 이벤트 리스너를 설정하여 UI에 대한 사용자의 액션 이벤트를 view에서 받을 수있다 (자세한 내용은 이후에)

다음이 애플리케이션의 예 :

	window.App = Ember.Application.create();

네임 스페이스는 어떤 이름으로도 문제가 안되지만 바인딩을 인식하기 위해 대문자로 시작되어야한다.

만약 Ember 애플리케이션을 현존하는 사이트에 넣으려 할 때 특정 요소에 대해 `rootElement`속성을 사용하여 이벤트 리스너를 설정 할 수있다 :

	window.App = Ember.Application.create({
		rootElement: '#sidebar'
	});

## UI를 Handlebars를 사용하여 표현하기

### Handolebars

Ember에는 시맨틱 템플릿 언어인 [Handlebars (http://handlebarsjs.com/)가 번들되어있다. 이 템플릿은 일반 HTML에 표현식이 포함 된 것과 같은 모양이된다.

Handlebars 템플릿은 애플리케이션내의 HTML 파일에 저장해야 하며, 런타임에 Ember는 템플릿을 컴파일하고 view내에서 사용할 수 있도록한다.

		<html>
		<body>
			<script type="text/x-handlebars">
				Hello, <b>{{MyApp.name}}</b>
			</script>
		</body>
		</html>

나중에 사용할 템플릿을 설정하려면 `<script>`태그에 `data-template-name`속성을 추가 :

	<html>
		<head>
			<script type="text/x-handlebars" data-template-name="say-hello">
			Hello, <b>{{MyApp.name}}</b>
			</script>
		</head>
	</html>

### Ember.View

`Ember.View`를 이용해 Handlebars 템플릿을 DOM에 삽입 할 수도있다.

view에 대해 어떤 템플릿을 사용할지 여부를 지정하기 위하여는 `templateName`속성에 지정하면된다. 만약 `<script>`태그가 다음과 같다면 :

	<html>
		<head>
			<script type="text/x-handlebars" data-template-name="say-hello">
				Hello, <b>{{name}}</b>
			</script>
		</head>
	</html>

`templateName`속성을 `"say-hello"`로 설정한다.

	var view = Ember.View.create({
		templateName: 'say-hello',
		name: "Bob"
	});

주의 :이 설명서 아래에서는 `templateName`속성은 대부분의 경우에서 생략하고 있다. `Ember.View`와 Handlebars의 템플릿을 사용한 코드 샘플 내에서는 view는 `templateName`속성을 사용하고 템플릿을 사용하여 표시되고 있다고 생각해주기 바란다.

`appendTo`를 통해 view를 문서에 부여 할 수있다 :

	  view.appendTo('#container');

`append`축약메서드를 사용하여 문서 바디에 추가 할 수있다 :

	view.append();

문서로부터 view를 제거하려면 `remove`를 이용한다 :

	view.remove();

### Handlebars: 기본

지금까지 본 바와 같이, Handlebars의 식 또는 중괄호 내('{{}}')에 속성을 지정하여 그 값을 표시 할 수있다 :

	My new car is {{color}}.

위의 예에서는 View내의 `color`속성을 검색하고 표시한다. 예를들어 view가 다음같다면 :

	App.CarView = Ember.View.extend({
		color: 'blue'
	});

view는 브라우저에서 다음과 같이 표시된다 :

	My new car is blue.

또한 전역 경로를 지정할 수도있다 :

	My new car is {{App.carController.color}}.

(Ember에서는 경로가 글로벌이거나 View 에 대해 상대적인지를 시작 문자가 대문자 인지의 여부로 판정한다. 따라서`Ember.Application`인스턴스가 대문자로 시작해야 한다.)

이 설명서내에서 설명하는 특징은 모두 바인딩 할 수있다는 것이다. 그말은 만약 템플릿내에서 사용되는 값이 변경되면 HTML도 마법처럼 자동으로 업데이트된다.

내재된 속성의 변경에 의해 HTML내의 어떤 부분이 업데이트되는지를 알기 위해서 Handlebars는 유일한 ID를 사용하여 마커 요소를 추가한다. 애플리케이션이 실행하는 동안 확인하면 다음과 같은 추가 요소를 알아챌 수 있을 것이다 :

	My new car is
	<script id="metamorph-0-start" type="text/x-placeholder"></script>
	blue
	<script id="metamorph-0-end" type="text/x-placeholder"></script>.

Handlebars식이 이 마커에 둘러싸여 있기 때문에, HTML 태그는 동일한 블록 내에 있을 필요가 있다. 예를들어 다음과 같이 해서는 안된다 :

	<!-- Don't do it! -->
	<div {{#if }}class="urgent"{{/if}}>

만약 속성의 출력를 마커로 묶고 싶지 않은 경우는 `unbind`헬퍼를 이용한다 :

	My new car is {{unbound color}}.

출력으로부터 마커는 제거되지만 자동 업데이트는 되지않기 때문에 주의가 필요하다.

	My new car is blue.

### {{#if}}, {{else}} 와 {{#unless}}

속성이 존재하는 경우에만 템플릿에 있는 특정 부분을 표시하고 싶은 경우가 있다. 예를들면, view에 `firstName`와 `lastName`객체를 포함한 `person`속성이 있다고 하면 :

	App.SayHelloView = Ember.View.extend({
		person: Ember.Object.create({
			firstName: "Joy",
			lastName: "Clojure"
		})
	});

`person`객체가 존재하는 경우에만 템플릿의 어떤 부분을 표시하기 위해서는 `{{# if}}`헬퍼를 사용하여 블록 렌더링에 조건을 부여 할 수있다 :

	{{#if person}}
		Welcome back, <b>{{person.firstName}} {{person.lastName}}</b>!
	{{/if}}

Handlebars 는 매개변수가 `false`, `undefined`, `null` 또는 `[]`(그 어떤false값이라도)라고 판정되는 경우에 이 블록을 렌더링 하지 않는다.

`{{else}}`를 사용하여 식이 false가 되는 경우에 다른 템플릿을 사용해 표시를 한다.:

	{{#if person}}
		Welcome back, <b>{{person.firstName}} {{person.lastName}}</b>!
	{{else}}
		Please log in.
	{{/if}}

`{{#unless}}`를 사용하여 값이 false 일때만 표시하는 블록을 지정가능하다 :

	{{#unless hasPaid}}
		You owe: ${{total}}
	{{/unless}}

`{{# if}}`와`{{# unless}}`는 블록 식의 예이다. 이들은 템플릿내의 일부에서 헬퍼를 실행하는 것을 가능하게 한다. 블록 식은 일반 식과 유사한 외형이지만 헬퍼 이름 앞에 해시 (#)를 포함하고 식을 닫을 필요가 있다.

### {{#with}}

템플릿 섹션를 `Ember.View`가 아닌 컨텍스트에서 실행하고 싶은 경우가 있다. 예를들어, `{{# with}}`헬퍼를 사용하여 위의 예제 템플릿을 구성 할 수있다 :

	{{#with person}}
		Welcome back, <b>{{firstName}} {{lastName}}</b>!
	{{/with}}

`{{# with}}`에서는 블록의 컨텍스트를 변경할 수있다. 컨텍스트는 어떤 객체의 속성을 찾을것인가의 지정한다. 기본값 컨텍스트는 템플릿이 속한 `Ember.View`이다.

### {{bindAttr}}를 사용하여 요소의 속성을 바인딩한다.

텍스트 이외에도 템플릿내의 HTML 요소의 특성을 지정하는 경우가 있다. 예를들어 URL을 포함 view를 지정 하는 경우를 생각하면 :

	App.LogoView = Ember.View.extend({
		logoUrl: 'http://www.mycorp.com/images/logo.png'
	});

Handlebars내에서 URL을 이미지로 표시하는 가장 좋은 방법은 다음과 같다 :

	<div id="logo">
		<img {{bindAttr src ="logoUrl"}} alt="Logo">
	</div>

그리고 이것은 다음 HTML을 생성한다 :

	<div id="logo">
		<img src="http://www.mycorp.com/images/logo.png" alt="Logo">
	</div>

`{{bindAttr}}`을 부울 값으로 사용하는 경우, 속성을 추가하거나 삭제한다. 예를들면 다음 Ember view에서는 :

	App.InputView = Ember.View.extend({
		isDisabled: true
	});

그리고 템플릿에는 :

	<input type="checkbox" {{bindAttr disabled="isDisabled"}}>

Handlebars는 다음 HTML을 생성한다 :

	<input type="checkbox" disabled>

### {{bindAttr}}를 사용하여 클래스 이름을 바인딩

`class`속성은 다른 속성처럼 바인딩 할 수있다. 하지만 특수한 동작도 추가된다. 기본 동작은 예상 한대로 :

JS:

	App.AlertView = Ember.View.extend({
		priority: "p4",
		isUrgent: true
	});

HTML: 

	<div {{bindAttr ="priority"}}>
		Warning!
	</div>

이 템플릿은 다음 HTML을 출력한다 :

	<div class="p4">
		Warning!
	</div>

바인딩 값이 부울의 경우 대시가 추가된 속성이 클래스로 취급된다. :

	<div {{bindAttr class="isUrgent"}}>
		Warning!
	</div>

이 템플릿은 다음 HTML을 출력한다 :

	<div class="is-urgent">
		Warning!
	</div>

다른 속성 값과 달리 여러 클래스를 바인딩 할 수도있다 :

	<div {{bindAttr class="isUrgent"}}>
		Warning!
	</div>

대시 추가 방식의 클래스 이름 외에 자유롭게 이름을 지정할 수도있다 :

	<div {{bindAttr class="isUrgent:urgent"}}>
		Warning!
	</div>

이 경우에는`isUrgent`속성이 true 로 되는 경우 `urgent`클래스가 추가되고 만약 거짓 경우 `urgent`클래스가 삭제된다.

### {{action}}을 사용하여 이벤트를 처리

`{{action}}`헬퍼를 사용하여 요소에서 발생하는 이벤트를 view 클래스에 부여한다 :

`click`이벤트를 `edit()`에 부여 :

	<a href="#" {{action "edit" on="click"}}>Edit</a>

`click`이벤트는 기본 이벤트이기에, 다음과 같이 더 짧게 작성 할 수도있다 :

	<a href="#" {{action "edit"}}>Edit</a>

`{{action}}`헬퍼를 포함 view를 디폴트 대상으로하지만, 다른 view를 대상으로 할 수도있다 :

	<a href="#" {{action "edit" target="parentView"}}>Edit</a>

액션 핸들러는 jQuery의 이벤트 객체를 받아 들일 수도 있고, `view`와 `context`속성을 확장한다. 이러한 속성은 다른 view를 대상으로하는 경우에 유용하다. 예 :

	App.ListingView = Ember.View.extend({
		templateName: 'listing',
		edit: function(event) {
			event.view.set('isEditing', true);
		}
	});

위에있는 템플릿은 모두 다음 HTML을 생성한다 :

	<a href="#" data-ember-action="3">Edit</a>

Ember는 내부적으로 설정된`data-ember-action`id 를 통해 대상 view의 이벤트를 위임한다.

### View의 계층 구조를 만든다

지금까지는 하나의 뷰에 대해 템플릿을 쓰는 방법을 봐왔다. 그러나 애플리케이션 개발을 진행시켜 나가는 중에 페이지의 다른 영역에 view 계층 구조를 캡슐화할 필요를 느끼는 경우가 있다. 각각의 view가 표시하는 속성의 유지 보수 그리고 이벤트 관리를 담당 할 필요가 있다.

### {{view}}

`{{view}}`헬퍼를 사용하여 부모에 대해서 자식이 될 view를 추가 가능하다. `{{view}}`헬퍼에는 view 클래스의 경로를 지정한다.

JS: 

	// Define parent view
	App.UserView = Ember.View.extend({
		templateName: 'user',
		firstName: "Albert",
		lastName: "Hofmann"
	});
	// Define child view
	App.InfoView = Ember.View.extend({
		templateName: 'info',
		posts: 25,
		hobbies: "Riding bicycles"
	});

HTML:

	User: {{firstName}} {{lastName}}
	{{view App.InfoView}}

HTML:

	<b>Posts:</b> {{posts}}
	<br>
	<b>Hobbies:</b> {{hobbies}}

만약 `App.UserView`의 인스턴스를 생성하여 렌더링했다고하면 DOM에서는 다음과 같이 취급된다 :

	User: Albert Hofmann
	<div>
		<b>Posts:</b> 25
		<br>
		<b>Hobbies:</b> Riding bicycles
	</div>

#### 상대적 경로

절대 경로 대신 어느 view 클래스를 사용할 지 부모가 될 view에서 상대 경로로 지정할 수도있다.
예를들어 위의 view 계층 구조를 다음과 같이 하는 것도 가능 :

JS: 

	App.UserView = Ember.View.extend({
		templateName: 'user',
		firstName: "Albert",
		lastName: "Hofmann",
		infoView: Ember.View.extend({
			templateName: 'info',
			posts: 25,
			hobbies: "Riding bicycles"
		})
	});

HTML:

	User: {{firstName}} {{lastName}}
	{{view infoView}}

Ember는 대문자로 시작하는 속성을 글로벌로 처리하므로, view 클래스를 이렇게 중첩 상태로 하는 경우 소문자를 사용할 것.

### 자식이 될 view 템플릿 의 설정

메인 템플릿내에서 자식이 될 View를 인라인으로 지정하려는 경우에는 블록 형식의 `{{#view}}`헬퍼를 사용할 수있다. 위의 예라면 다음과 같이 고쳐 쓸 수 있다. :

JS:

	App.UserView = Ember.View.extend({
		templateName: 'user',
		firstName: "Albert",
		lastName: "Hofmann"
	});
	App.InfoView = Ember.View.extend({
		posts: 25,
		hobbies: "Riding bicycles"
	});

HTML:

	User: {{firstName}} {{lastName}}
	{{#view App.InfoView}}
		<b>Posts:</b> {{posts}}
		<br>
		<b>Hobbies:</b> {{hobbies}}
	{{/view}}

이렇게 처리하는 경우에는 페이지의 한 부분에 대해 view를 할당하고 있다고 생각하면 좋다. 이렇게하는 것으로 이벤트 핸들링을 그 페이지내의 한 부분에 캡슐화 하는것도 가능.

### 바인딩의 설정

여기까지의 예에서는 view에 대해 정적 값을 설정했지만, MVC 구조를 구현하는 가장 좋은 방법은 View 의 속성을 Controller 레이어에 바인딩하는 방법이다.

그럼 Controller가 사용자 데이터를 표현하도록 설정해 보자 :

	App.userController = Ember.Object.create({
		content: Ember.Object.create({
			firstName: "Albert",
			lastName: "Hofmann",
			posts: 25,
			hobbies: "Riding bicycles"
		})
	});

`App.UserView`를 업데이트하고`App.userController`에 바인딩 해 보자 :

	App.UserView = Ember.View.extend({
		templateName: 'user',
		firstNameBinding: 'App.userController.content.firstName',
		lastNameBinding: 'App.userController.content.lastName'
	});

`App.UserView`의 예처럼 적게 바인딩을 설정하려면 템플릿내에서 이러한 바인딩을 선언하는 것이 편한 경우도 있다. `{{# view}}`헬퍼에 추가 인수를 전달하여 그렇게 하는 것도 가능. 만약 바인딩 설정밖에 하고 있지 않으면 이 기능을 사용하는 것으로 새로운 서브 클래스를 만드는 것을 피할 수 있다.

	User: {{firstName}} {{lastName}}
	{{#view App.UserView postsBinding="App.userController.content.posts"
		hobbiesBinding="App.userController.content.hobbies"}}
		<b>Posts:</b> {{posts}}
		<br>
		<b>Hobbies:</b> {{hobbies}}
	{{/view}}

주의 :`{{view}}`의 인수로 바인딩 뿐만 아니라 어떤 속성이라도 전달할 수 있지만, 바인딩의 설정 이외의 구현이 필요한 경우는 서브 클래스를 작성하는 것이 더 좋은 방법이라 할 수있다.

### View의 HTML을 수정

view를 삽입 할 때 콘텐츠를 추가 한 상태의 HTML 요소가 생성된다. 만약 view가 자식이 될 view를 가지는 경우, 부모의 HTML 요소 안에 자식 노드로 표시된다.

디폴트에서는 새로운`Ember.View`인스턴스는`<div>`요소를 생성하지만,`tagName`매개 변수를 사용하여 재정의 할 수도있다 :

	{{view App.InfoView tagName="span"}}

`id`매개 변수를 전달하여 HTML 요소에 대해 ID 속성을 지정할 수도 있다 :

	{{view App.InfoView id="info-view"}}

이렇게하는 것으로 CSS의 ID 셀렉터를 사용하여 쉽게 스타일을 추가 할 수있다 :

	/** Give the view a red background. **/
	#info-view {
		background-color: red;
	}

마찬가지로 클래스 이름을 지정할 수도 있다 :

	{{view App.InfoView class="info urgent"}}

클래스 이름은 view 속성에 대해 `class`대신 `classBinding`을 통해 바인딩 할 수도 있다. 이렇게하는 것으로`bindAttr`가 가지는 동작과 같은 동작을 적용 할 수있다 :

JS:

	App.AlertView = Ember.View.extend({
		priority: "p4",
		isUrgent: true
	});

HTML:

	{{view App.AlertView classBinding="isUrgent priority"}}

이렇게하는 것으로 view wrapper는 다음과 같은 결과가 된다 :

	<div id="sc420" class="sc-view is-urgent p4"></div>

### 목록 항목을 표시하기

객체의 목록을 나열하려면 Handlebars의 `{{# each}}`헬퍼를 이용한다 :

JS:

	App.PeopleView = Ember.View.extend({
		people: [ { name: 'Yehuda' },
		{ name: 'Tom' } ]
	});

HTML:

	<ul>
		{{#each people}}
		<li>Hello, {{name}}!</li>
		{{/each}}
	</ul>

아래와 같이 리스트를 표시:

	<ul>
		<li>Hello, Yehuda!</li>
		<li>Hello, Tom!</li>
	</ul>

목록의 모든 항목에 대해 view를 만들려면 현재 컨텍스트에 view내의 속성을 바인딩 할 수도 있다.
예를들어, 다음 예에서는 목록의 모든 항목에 대해 view을 만들고 그 항목에 대해 `content`속성을 설정한다 :

	{{#each App.peopleController}}
		{{#view App.PersonView contentBinding="this"}}
		{{content.firstName}} {{content.lastName}}
		{{/view}}
	{{/each}}

### 사용자 정의 헬퍼를 만드는 방법

애플리케이션내에서 같은 HTML을 사용하는 경우는 많지만, 이런 경우에 Handlebars 의 템플릿내에서 수행 할 수있는 사용자 정의 헬퍼를 등록 할 수있다.

예를들어 특정 값에 대해 자주 `<span>`태그에 사용자 정의 클래스를 추가하는 케이스에 다음과 같이 JavaScript로부터 사용자 정의 헬퍼를 등록 할 수있다 :

	Handlebars.registerHelper('highlight', function(property) {
		var value = Ember.getPath(this, property);
		return new Handlebars.SafeString('<span class="highlight">'+value+'</span>');
	});

HTML을 헬퍼로부터 반환하는 경우, 그리고 이스케이프하고 싶지 않은 경우에는`SafeString`를 리턴할 것.

Handlebars 템플릿내에서 이 헬퍼를 실행할 수 있다. :

	{{highlight name}}

그리고 다음과 같이 출력된다 :

	<span class="highlight">Peter</span>

주의 : 헬퍼 함수에 대해 전달 된 매개 변수는 현재 값으로서뿐만 아니라 name으로 전달된다. 이렇게하는 것으로 값에 대해 옵저버를 설정하는 것이 가능하게된다. 매개 변수의 현재 값을 얻으려면 위의 예와 같이 'Ember.getPath`를 사용할 것.

### 설정된 View

Ember는 텍스트 입력과 체크 박스, 풀다운 메뉴 등의 기본적인 컨트롤 세트가 패키지 되어있다.

아래에 예를 보여준다 :

#### Ember.Checkbox

	<label>
		{{view Ember.Checkbox checkedBinding="content.isDone"}}
		{{content.title}}
	</label>

#### Ember.TextField

	App.myText = Ember.TextField.extend({
        formBlurredBinding: 'App.adminController.formBlurred',
        change: function(evt) {
          this.set('formBlurred', true);
        }
      });

#### Ember.Select

    {{view Ember.Select viewName="select"
                          contentBinding="App.peopleController"
                          optionLabelPath="content.fullName"
                          optionValuePath="content.id"
                          prompt="Pick a person:"
                          selectionBinding="App.selectedPersonController.person"}

#### Ember.TextArea

    var textArea = Ember.TextArea.create({
            valueBinding: 'TestObject.value'

위의 컨트롤을 View에 추가하려면, 상기처럼 사용하는 것을 권장하고있다.

이벤트는 서브 뷰로부터 부모가되는 View에 대해 버블링하지 않기 때문에 이렇게 View를 확장하는 것이 그런 이벤트를 캡처하는 유일한 방법이 된다.

예:

	App.myText = Ember.TextField.extend({
		formBlurredBinding: 'App.adminController.formBlurred',
		change: function(evt) {
			this.set('formBlurred', true);
		}
	});

이렇게하는 것으로 이 view를 하위 view로 사용할 수 있고, 또한 이벤트를 캡처 할 수있다. 다음 예에서는 Name 의 변화가 폼에 대한 포커스를 빼앗고, 저장 버튼을 표시한다.

	<script id="formDetail" data-template-name='formDetail' type="text/x-handlebars">
	<form>
	<fieldset>
		<legend>Info:</legend>
		{{view App.myText name="Name" id="Name" valueBinding="myObj.Name"}}
		<label for="Name">Name</label><br/>
			{{#if formBlurred}}
			<a href="#" {{action "syncData" on="click"}}>Save</a>
			{{/if}}
	</fieldset>
	</form>
	</script>

## View를 좀 더 탐구

Handlebars의 처리에 익숙해졌으면 이벤트 처리와 요구에 따른 view의 사용자 정의 방법에 대해 보고가자.

### 이벤트 핸들러

이벤트 리스너를 요소에 대해 등록하는 대신 view내의 메서드로 이벤트 명을 구현하고자한다.

예를들어 다음과 같은 템플릿이 있다고하고 :

	{{#view App.ClickableView}}
		This is a clickable area!
	{{/view}}

`App.ClickableView`을 클릭하면 alert을 표시시켜 보자 :

	App.ClickableView = Ember.View.extend({
		click: function(evt) {
			alert("ClickableView was clicked!");
		}
	});

이벤트 대상 view로부터 각각의 부모가 될 view에 대해 읽기 전용이 될 값이 루트 값으로 설정되어 있지 않는 한 연속해서 버블업 해나간다. 만약 JavaScript를 사용하여 (handlebars의`{{view}}`을 사용하지 않고 작성했다고 하고) View를 관리하는 경우에는 다음 `Ember.ContainerView`에 대한 문서를 읽기 바란다.

### `Ember.ContainerView`를 통해 view를 수동으로 관리

보통이라면 view는 자식이 될 view를`{{view}}`헬퍼를 사용하여 생성하지만, 수동으로 view의 자식이 될 view를 관리하는 것이 편리한 경우도​​있다.
`Ember.ContainerView`의 인스턴스를 만들고 `childViews`배열이 추가 된 경우, 추가한 View 페이지내에서 렌더링 되고, 삭제된 view는 DOM에서 제거된다.

	var container = Ember.ContainerView.create();
	container.append();
	var coolView = App.CoolView.create(),
	childViews = container.get('childViews');
	childViews.pushObject(coolView);

축약어 형태로 자식이 될 view를 속성으로 지정할 수도 있고, 키 목록으로 지정할 수도 있다. container view가 생성 될 때 이 view는 초기화 되어, 자식이 될 view 배열에 추가된다 :

	var container = Ember.ContainerView.create({
		childViews: ['firstView', 'secondView'],
		firstView: App.FirstView,
		secondView: App.SecondView
	});

### render 메서드의 공급원

View가 DOM 요소로 변환되기 이전에, view는 문자열로 표현된 것에 지나지 않는다. view가 렌더링 될 때마다 각각의 자식이 될 view를 문자열로 결합하고있다.

만약 Handlebars 이외의 템플릿 엔진을 사용하는 경우, view의 `render`메서드를 재정의 하는것으로 HTML 사용자 지정 문자열을 생성 할 수있다.

	App.CoolView = Ember.View.create({
		render: function(buffer) {
			buffer.push("<b>This view is so cool!</b>");
		}
	});

이렇게하는 것으로 Handlebars 이외의 템플릿 엔진을 지원하는 것을 허용하고 있지만, 렌더링을 재정의 하는것으로 값의 자동 업데이트는되지 않기 때문에주의가 필요하다. 모든 업데이트는 직접 구현할 필요가있다.

### HTML 요소의 사용자 정의

하나의 view는 하나의 DOM 요소로 페이지 내에서 표현된다. `tagName`속성을 변경하여 어느 요소가 생성되는지를 변경할 수있다.

	App.MyView = Ember.View.extend({
		tagName: 'span'
	});

또 똑같이 클래스 명도`className`속성을 문자열 배열로 지정하는 것으로 변경 할 수있다 :

	App.MyView = Ember.View.extend({
		classNames: ['my-view']
	});

view 의 속성 상태에 따라 클래스명을 결정하고 싶은 경우에는 클래스명의 바인딩을 이용할 수 있다. 만약 부울값에 바인딩하면 클래스명은 값에 따라 추가되거나 삭제된다 :

	App.MyView = Ember.View.extend({
		classNameBindings: ['isUrgent'],
		isUrgent: true
	});

위의 예을 렌더링하면 다음과 같다 :

	<div class="ember-view is-urgent">

만약 `isUrgent`가 false로 변경되면 클래스명 `is-urgent`는 삭제된다.

부울 값을 갖는 속성에 대시를 붙인 클래스명이 추가되지만, 콜론을 사용하여 클래스 명을 변경할 수도있다 :

	App.MyView = Ember.View.extend({
		classNameBindings: ['isUrgent:urgent'],
		isUrgent: true
	});

다음 HTML 로 렌더링된다 :

	<div class="ember-view urgent">

바인딩 된 값이 문자열인 경우 변경없이 값이 클래스 이름으로 추가된다.

### View내의 속성 바인딩

`attributeBindings`을 이용하여 view를 표현하는 DOM 요소의 속성을 바인딩 할 수있다.

	App.MyView = Ember.View.extend({
		tagName: 'a',
		attributeBindings: ['href'],
		href: "http://emberjs.com"
	});


## THE EMBER ENUMERABLE API

### Enumerables이란?

Ember 내에서는 Enumerables라는것은 자식 객체를 여럿 가지는 객체 모두이며 그 자식 객체에 대해 Enumerables 인터페이스를 통해 액세스 할 수 있게하는 것을 가리킨다. 가장 기본적인 Enumerables는 JavaScript의 빌트인 배열이다.

예를들어 모든 Enumerables는 표준인 `forEach`메서드를 지원하고있다 :

	[1,2,3].forEach(function(item) {
		console.log(item);
	});

일반적으로는`forEach`와 같은 Enumerables 메서드는 2 번째의 필수가 아닌 인수를 받아, 콜백 함수 내에서 `this`의 값이 된다.

	var array = [1,2,3];
	array.forEach(function(item) {
		console.log(item, this.indexOf(item));
	}, array)

그 밖에도 이유가 있지만, 이렇게하는 것으로 다른 Enumerables 메서드를`forEach`의 콜백으로 사용할 수있게 되는 점은 매우 편리하다 :

	var array = [1,2,3];
	array.forEach(array.removeObject, array);

주의 : 이 두 번째 인수는 이 같이 메서드을 사용한 경우의 JavaScript가 `this`의 값을 `window`에 할당하는 동작의 제2의 해결책이 된다. (아 뭔말인지 모르것다 -_-)

### Ember내의 Enumerables

Ember 객체내에서 목록을 나타내는 객체는 대개의 경우 Enumerables 인터페이스를 구현하고있다. 몇 가지 예를 보자 :

- *배열* : Ember는 네이티브 JavaScript 배열을 Enumerables 인터페이스를 통해 확장하고있다.
- *배열 프록시* : 네이티브 배열을 래핑하여 view 레이어용으로 추가의 기능을주는 구성 개념.
- *Set* : 객체가 객체를 포함할지 여부에 대해 신속하게 회답한다.

### Enumerables인터페이스

#### 매개변수

Enumerables 메서드의 콜백은 다음 3 개의 인수를 사용 :

- *item*: 현재 이터레이션 항목.
- *index*: 정수 값. 0부터 카운트된다.
- *self*: Enumerables 그 자체

#### 나열

Enumerable 객체의 모든 값을 열거하려면 `forEach`메서드를 사용한다. :

	enumerable.forEach(function(item, index, self) {
		console.log(item);
	});

Enumerable 객체의 요소인 메서드을 실행하고 싶은 경우에는 `invoke`메서드를 사용한다. :

	Person = Ember.Object.extend({
		sayHello: function() {
			console.log("Hello from " + this.get('name'));
		}
	});
	var people = [
	Person.create({
		name: "Juan"
	}), Person.create({
		name: "Charles"
	}), Person.create({
		name: "Majd"
	})]
	people.invoke('sayHello');
	// Hello from Juan
	// Hello from Charles
	// Hello from Majd

#### First와last

`firstObject`또는`lastObject`을 이용하여 Enumerable로부터 처음과 마지막 객체를 얻을 수 있다 :

	[1,2,3].get('firstObject') // 1
	[1,2,3].get('lastObject')  // 3

#### 배열로 변환

`toArray`메서드를 사용하여 Enumerable로부터 배열을 생성 할 수있다.

#### 변환

`map`메서드를 사용하면 Enumerable를 바탕으로 한 배열로 변환 할 수있다.:

	['Goodbye', 'cruel', 'world'].map(function(item, index, self) {
		return item + "!";
	});
	// returns ["Goodbye!", "cruel!", "world!"]	

#### 각 객체의 set과 get

`forEach`나`map`은 각 요소의 속성을 get 또는 set 할 때 자주 사용된다. `getEach`와`setEach`메서드를 이용하여 그 목적을 달성 할 수 있다 :

	var arr = [Ember.Object.create(), Ember.Object.create()];
	// we now have an Array containing two Ember.Objects
	arr.setEach('name', 'unknown');
	arr.getEach('name') // ['unknown', 'unknown']

#### 필터링

Enumerable 에 대해 자주하는 작업으로는 Enumerable를 입력하고, 특정 규칙에 의해 필터링 된 배열을 반환하는 구현이다.

필터링에는 (예상대로)`filter`메서드를 이용할 수있다. 이 메서드는 콜백 내에서`true`를 돌려주는 것을 기대하고있다.콜백이`true`를 돌려 주면 Ember 최종 배열 내에 그 값를 저장하고`false`또는`undefined`가되는 경우는 Ember는 값을 배열에 저장하지 않는다.

	var arr = [1,2,3,4,5];
	arr.filter(function(item, index, self) {
		if (item < 4) { return true; }
	})
	// returns [1,2,3]

Ember 객체의 컬렉션을 조작하는 경우, 어떤 속성 값을 참고로 객체의 집합을 필터링하고 싶다고 생각 할 것이다. 그런 경우에는`filterProperty`메서드가 숏컷을 제공 해주고있다.

	Todo = Ember.Object.extend({
		title: null,
		isDone: false
	});
	todos = [
	Todo.create({
		title: 'Write code',
		isDone: true
	}), Todo.create({
		title: 'Go to sleep'
	})];
	todos.filterProperty('isDone', true);
	// returns an Array containing just the first item

일치하는 값을 포함하는 배열을 반환하는 것이 아니라 처음에 일치하는 값을 반환하고 싶은 경우에는`find`와`findProperty`메서드를 이용할 수있다. 이들은`filter`와`filterProperty`처럼 동작하지만, 1 개의 아이템 만 반환한다.

#### 정보의 Aggregation (all 또는 any)

Enumerable에 있는 모든 항목이 특정 조건에 부합 하는지를 알아내기 위해서는 `every`메서드를 사용할 수 있다. :

	Person = Ember.Object.extend({
		name: null,
		isHappy: false
	});
	var people = [
	Person.create({
		name: 'Yehuda',
		isHappy: true
	}), Person.create({
		name: 'Majd',
		isHappy: false
	})];
	people.every(function(person, index, self) {
		if (person.get('isHappy')) {
			return true;
		}
	});
	// returns false

또는 Enumerable내의 최소한 하나의 항목이 조건에 일치하는 여부를 확인하려면 `some`메서드를 사용할 수 있다. :

	people.some(function(person, index, self) {
		if(person.get('isHappy')) { return true; }
	});
	// returns true

필터링 방법과 마찬가지로`every`와`some`메서드는 `everyProperty`와 `someProperty`라는 유사한 메서드를 가지고있다 :

	people.everyProperty('isHappy', true) // false
	people.someProperty('isHappy', true)  // true
