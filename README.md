# contactsapp

## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```

### Lints and fixes files
```
npm run lint
```

### 비주얼 스튜디오 README.md 여는법
Ctrl + Shift + V  

## EventBus
상위 컴포넌트(eventBus.$on) - 중간 지점(EventBus.js) - 하위 컴포넌트(eventBus.$emit)

### 동작 원리
1. 하위 컴포넌트에서 이벤트 호출
2. 상위 컴포넌트에서 이벤트 등록

<br>
ex)  

하위 컴포넌트 호출
``` javascript
submitEvent : function() {
      if(this.mode == "update") {
        eventBus.$emit("updateSubmit", this.contact);
      } else {
        eventBus.$emit("addSubmit", this.contact); // 이벤트 호출
      }
    },
```
상위 컴포넌트 등록
``` javascript
eventBus.$on("addSubmit", (contact) => { // 이벤트 등록
            this.currentView = null;
            this.addContact(contact);
        });
```

## 동적 컴포넌트
데이터의 값에 따라 컴포넌트를 변화

```html
<!-- html -->

<div id="container">
      <!-- <div class="page-header">
          <h1 class="text-center">연락처 관리 어플리케이션</h1>
          <p>(Dynamic Component + EventBus + Axios)</p>
      </div> -->
      <component :is="currentView" :contact="contact"></component>
      <!-- <contactList :contactlist="contactlist"></contactList> -->
  </div>
```
``` javascript
eventBus.$on("updateSubmit", (contact) => {
            this.currentView = null;               // null 일때
            this.updateContact(contact);
        });
        eventBus.$on("addContactForm", () => {
            console.log("새로운 연락처 추가 on")     
            this.currentView = 'addContact';       // 연락처 추가 버튼을 눌렀을때 
            console.log(this.currentView)
        });
        eventBus.$on("editContactForm", (no) => {
            this.fetchContactOne(no)
            this.currentView = 'updateContact';    // 편집 버튼을 눌렀을때
        });
```

