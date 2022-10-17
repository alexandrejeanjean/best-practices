
## The rules of the house : Boy scout rules -> ***Leave the campground cleaner that you found it.***

- Let a clear todo statement when a work is not finish/complet (if test is missing, or inline style can be exctracted in module css).
- When working is in progress start you commit with **[WIP] your awesome commit**
- ON THE IMPORTANCE OF COMMIT MESSAGE: Your commit msg cannot be too long. Give a description of **WHY** (not what) (how, if its hard) have you do that.
- When merging two branch, use the `-m` flag to add a commit
- Every pure function should be unit tested

# React best practices

### Use JSX / TSX ShortHand

Prefer this

```
return(
  <Navbar showTitle />  
)
```

rather than that

```
return (
  <Navbar showTitle={true} />
);
```

### Use Ternary Operators

```
const { role } = user;

return role === ADMIN ? <AdminUser /> : <NormalUser />
```

rather than that

```
const { role } = user;

if (role === ADMIN) {
  return <AdminUser />
} else {
  return <NormalUser />
} 
```

### Use Object Literals

```
const {role} = user

const components = {
  ADMIN: AdminUser,
  EMPLOYEE: EmployeeUser,
  USER: NormalUser
};

const Component = components[role];

return <Componenent />;
```

rather than that

```
const {role} = user

switch(role){
  case ADMIN:
    return <AdminUser />
  case EMPLOYEE:
    return <EmployeeUser />
  case USER:
    return <NormalUser />
}
```

### Use Fragments

Prefer this

```
return (
  <>
     <Component1 />
     <Component2 />
     <Component3 />
  </>  
)
```

rather than that

```
return (
  <div>
     <Component1 />
     <Component2 />
     <Component3 />
  </div>  
)
```

### Don't Define a Function Inside Render

Prefer this

```
const submitData = () => dispatch(ACTION_TO_SEND_DATA)

return (
  <button onClick={submitData}>  
    This is a good example 
  </button>  
)
```

rather than that

```
return (
    <button onClick={() => dispatch(ACTION_TO_SEND_DATA)}>    // NOTICE HERE
      This is a bad example 
    </button>  
)
```

### Use Memo

***React.PureComponent and Memo can significantly improve the performance of your application. They help us to avoid unnecessary rendering.***

Prefer this

***Here no matter how many times you click on the button, it will render only when necessary.***

```
const submitData = () => dispatch(ACTION_TO_SEND_DATA)

import React ,{useState} from "react";

const ChildrenComponent = React.memo(({userName}) => {
    console.log('rendered')
    return <div> {userName}</div>
})
```

rather than that

***The child component should render only once because the value of count has nothing to do with the ChildComponent.***
***But, it renders each time you click on the button.***

```
export const TestMemo = () => {
  const [userName, setUserName] = useState("faisal");
  const [count, setCount] = useState(0);
  
  const increment = () => setCount((count) => count + 1);
  
  return (
    <>
      <ChildrenComponent userName={userName} />
      <button onClick={increment}> Increment </button>
    </>
  );
};

const ChildrenComponent =({ userName }) => {
  console.log("rendered", userName);
  return <div> {userName} </div>;
};
```

### Put CSS in JavaScript

Prefer this

```
const bodyStyle = {
  height: "10px"
}

return <div style={bodyStyle}></div>
```

rather than that

```
// CSS FILE

.body {
  height: 10px;
}

//JSX

return <div className='body'>
   
</div>
```

### Use Object Destructuring

Prefer this

```
const { name, age, profession } = user;

return (
  <>
    <div> {name} </div>
    <div> {age} </div>
    <div> {profession} </div>
  </>  
)
```

rather than that

```
return (
  <>
    <div> {user.name} </div>
    <div> {user.age} </div>
    <div> {user.profession} </div>
  </>  
)
```

### String Props Don’t Need Curly Braces

Prefer this

```
return (
  <Navbar title="My Special App" />  
)
```

rather than that

```
return(
  <Navbar title={"My Special App"} />
)
```

### Remove JS Code From JSX / TSX

Prefer this

```
const onClickHandler = (event) => {
   console.log(event.target, 'clicked!'); 
}

return (
  <ul>
    {posts.map((post) => (
      <li onClick={onClickHandler} key={post.id}> {post.title} </li>
    ))}
  </ul>
);
```

rather than that

```
return (
  <ul>
    {posts.map((post) => (
      <li onClick={event => {
        console.log(event.target, 'clicked!'); // <- THIS IS BAD
        }} key={post.id}>{post.title}
      </li>
    ))}
  </ul>
);
```

### Use Template Literals

Prefer this

```
const userDetails = `${user.name}'s profession is ${user.proffession}`

return (
  <div> {userDetails} </div>  
)
```

rather than that

```
const userDetails = user.name + "'s profession is" + user.proffession

return (
  <div> {userDetails} </div>  
)
```

### Import in Order

***Always try to import things in a certain order. It improves code readability.***

Prefer this

***The rule of thumb is to keep the import order like this:***
***Built-in***
***External***
***Internal***

```
import React from 'react';

import { PropTypes } from 'prop-types';
import styled from 'styled-components/native';

import ErrorImg from '../../assets/images/error.png';
import colors from '../../styles/colors';
```

rather than that

```
import React from 'react';
import ErrorImg from '../../assets/images/error.png';
import styled from 'styled-components/native';
import colors from '../../styles/colors';
import { PropTypes } from 'prop-types';
```

### Use Implicit return

Prefer this

```
const add = (a, b) => a + b;
```

rather than that

```
const add = (a, b) => {
  return a + b;
}
```

### Component Naming

Prefer this

***Always use PascalCase for components and camelCase for instances.***

```
import ReservationCard from './ReservationCard';

const reservationItem = <ReservationCard />;
```

rather than that

```
import reservationCard from './ReservationCard';

const ReservationItem = <ReservationCard />;
```

### Component Naming

Prefer this

***Don’t use DOM component prop names for passing props between components because others might not expect these names.***

```
<MyComponent variant="fancy" />
```

rather than that

```
<MyComponent style="dark" />

<MyComponent className="dark" />
```

### Quotes

Prefer this

***Use double quotes for JSX attributes and single quotes for all other JS.***

```
<Foo bar="bar" />

<Foo style={{ left: '20px' }} />
```

rather than that

```
<Foo bar='bar' />

<Foo style={{ left: "20px" }} />
```

### Prop Naming

Prefer this

***Always use camelCase for prop names or PascalCase if the prop value is a React component.***

```
<MyComponent
  userName="hello"
  phoneNumber={12345678}
  Component={SomeComponent}
/>
```

rather than that

```
<Component
  UserName="hello"
  phone_number={12345678}
/>
```

### JSX in Parentheses

Prefer this

***If your component spans more than one line, always wrap it in parentheses.***

```
return (
    <MyComponent variant="long">
      <MyChild />
    </MyComponent>
);
```

rather than that

```
return <MyComponent variant="long">
           <MyChild />
         </MyComponent>;
```

### Self-Closing Tags

Prefer this

***If your component doesn’t have any children, then use self-closing tags. It improves readability.***

```
<SomeComponent variant="stuff" />
```

rather than that

```
<SomeComponent variant="stuff"></SomeComponent>
```

### Underscore in Method Name

Prefer this

```
const onClickHandler = () => {
  // do stuff
}
```

rather than that

```
const _onClickHandler = () => {
  // do stuff
}
```

Source : https://betterprogramming.pub/21-best-practices-for-a-clean-react-project-df788a682fb

Based on AirBnB Guidelines - https://github.com/airbnb/javascript/tree/master/react
