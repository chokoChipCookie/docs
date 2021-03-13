ES6_7_8_정리

버전업이 될때마다 새로운 메소드가 추가되며, 그로인해 기능이 늘어나고 편리해짐.

ES6	
	참고 : https://blog.asamaru.net/2017/08/14/top-10-es6-features/
	1. 변수 선언시 let, const 사용이 가능하다.
		let 은 변수에 재할당이 가능
		const는 변수 재선언, 변수 재할당 모두 불가능
	
	2. 템플릿 리터럴 (문자열 처리 방식이 간편해짐)
		예시
			기존
			var link = function (height, color, url) {
				var height = height || 50
				var color = color || 'red'
				var url = url || 'http://azat.co'
				...
			}
			
			ES6
			var link = function(height = 50, color = 'red', url = 'http://azat.co') {
			  ...
			}
		
		예시2
			기존
			var roadPoem = 'Then took the other, as just as fair,\n\t'
				+ 'And having perhaps the better claim\n\t'
				+ 'Because it was grassy and wanted wear,\n\t'
				+ 'Though as for that the passing there\n\t'
				+ 'Had worn them really about the same,\n\t'

			var fourAgreements = 'You have the right to be you.\n\
				You can only be you when you do your best.'
				
			ES6
			var roadPoem = `Then took the other, as just as fair,
				And having perhaps the better claim
				Because it was grassy and wanted wear,
				Though as for that the passing there
				Had worn them really about the same,`

			var fourAgreements = `You have the right to be you.
				You can only be you when you do your best.`
	
	3. 화살표 함수 사용이 가능하다.
	화살표 함수는 항상 익명 함수이며 this의 값을 현재 문맥에 바인딩 시킨다.
		예시
		기존 
		var _this = this
		$('.btn').click(function(event){
		  _this.sendData()
		})
		
		ES6
		$('.btn').click((event) => {
		  this.sendData()
		})
		
	4. 변수 선언방법이 다양해져 특정 변수의 값이 변할지, final 값인지 구분이 가능해졌다.
	
	5. Promise 사용 시 가독성이 좋다. 
		기존
		setTimeout(function(){
		  console.log('Yay!')
		  setTimeout(function(){
			console.log('Wheeyee!')
		  }, 1000)
		}, 1000)
		
		Promise
		var wait1000 =  ()=> new Promise((resolve, reject)=> {setTimeout(resolve, 1000)})
		wait1000()
			.then(function() {
				console.log('Yay!')
				return wait1000()
			})
			.then(function() {
				console.log('Wheeyee!')
			});
			

-ES7 / ES8 참고 
	: https://velog.io/@syoung125/%EA%B0%9C%EB%85%90%EA%B3%B5%EB%B6%80-1.-JavascriptES6%EB%9E%80-ES7%EA%B3%BC-%EC%B0%A8%EC%9D%B4%EC%A0%90			
ES7
	ES6 의 내용에서 	제곱연산자 (**) 등장
	
	Array.includes 배열에 해당 요소가 존재하는지 확인하는 메소드 등장
	

ES8 
	-참고 : https://joshua1988.github.io/web-development/javascript/js-async-await/
	async & await : 비동기 처리 패턴
		callback 함수와 promise 함수의 단점을 보완하고 가독성 향상
		문법 
			async function 함수명() {
			  await 비동기_처리_메서드_명();
			}
			
			예시
			function fetchItems() {
			  return new Promise(function(resolve, reject) {
				var items = [1,2,3];
				resolve(items)
			  });
			}

			async function logItems() {
			  var resultItems = await fetchItems();
			  console.log(resultItems); // [1,2,3]
			}
	
	객체의 좀 더 심화된 메소드 등장
		-Object.keys()에 대응되는 메소드인 Object.values()
		-Object.keys()와 Object.values()를 합쳐 놓은 Object.entries() 등
	문자열 단순 편의기능 추가
		-문자열 앞부분에 공백을 넣어 자리수를 맞춰주는 String.padStart()
		-문자열 뒷부분에 공백을 넣어 자리수를 맞춰주는 String.padEnd()
		-매개변수 마지막에 콤마를 붙이는 것 허용
	