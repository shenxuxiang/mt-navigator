# mt-navigator

A light-weight React mt-ad-space component with extremely easy API（只适用于移动端项目）. [Online Demo](https://shenxuxiang.github.io/mt-navigator/), welcome [code review](https://github.com/shenxuxiang/mt-navigator)

## Installation
```sh
npm install mt-navigator --save
```

## Usage
```js
import React, { PureComponent } from 'react';
import img1 from './static/images/11.jpg';
import img2 from './static/images/12.jpg';
import img3 from './static/images/13.jpg';
import img4 from './static/images/14.jpg';
import img5 from './static/images/15.jpg';
import img6 from './static/images/16.png';
import Navigator from 'navigator';
import './app.css';

const source = [
  {
    url: img1,
    text: '精选',
    label: 1,
  },
  {
    url: img2,
    text: '良品铺子',
    label: 2,
  },
  {
    url: img3,
    text: '乳饮酒水',
    label: 3,
  },
  {
    url: img4,
    text: '粮油米面',
    label: 4,
  },
  {
    url: img5,
    text: '纸品家清',
    label: 5,
  },
  {
    url: img6,
    text: '休闲食品',
    label: 6,
  },
  {
    url: img1,
    text: '时令生鲜',
    label: 7,
  },
  {
    url: img2,
    text: '美容个理',
    label: 8,
  },
];

export default class App extends PureComponent {
  constructor() {
    super();
    this.state = {
      indicator: 0,
      fixed: false,
    };
    this.fixed = false;
  }

  componentDidMount() {
    this.navOffsetTop = document.querySelector('.mt-navigator').offsetTop;
    window.addEventListener('scroll', this.handleScroll, false);
  }
  componentWillUnmount() {
    window.removeEventListener('scroll', this.handleScroll, false);
  }

  handleScroll = () => {
    const offsetTop = window.pageYOffset ||
      document.documentElement.scrollTop ||
      document.body.scrollTop;
    if (offsetTop >= this.navOffsetTop && !this.fixed) {
      this.setState({ fixed: true });
      this.fixed = true;
    } else if (offsetTop < this.navOffsetTop && this.fixed) {
      this.setState({ fixed: false });
      this.fixed = false;
    }
  }

  render() {
    return (
      <div className="container">
        <Navigator
          tabIndex={1}
          background="#f90"
          className={`nav-header${this.state.fixed ? ' fixed' : ''}`}
        >
          {
            source.map((item) =>
              <div 
                key={item.label}
                className="nav-list-item"
                onClick={() => {
                  console.log(item.label, 'index')
                }}
              >
                <img src={item.url} className="nav-list-item-img" />
                <div className="nav-list-item-text">{item.text}</div>
              </div>
            )
          }
        </Navigator>
        <div style={{ background: '#fff', height: 200 }}></div>
        <div style={{ background: '#ccc', height: 200 }}>{`${this.state.fixed}`}</div>
        <div style={{ background: '#f80', height: 200 }}></div>
        <div style={{ background: '#fff', height: 200 }}></div>
        <div style={{ background: '#f90', height: 200 }}></div>
        <div style={{ background: '#f80', height: 200 }}></div>
        <div style={{ background: '#fff', height: 200 }}></div>
        <div style={{ background: '#f90', height: 200 }}></div>
      </div>
    );
  }
}
```

## props

| param            | detail                                         | type     | default         |
| ---------------- | -----------------------------------------------| -------- | -------         |
| background       | component background style                     | string   | '#fff'          |
| tabIndex         | the currently activated tab                    | number   | 0               |
| children         | child node of component                        | array    | []              |
| className        | component class name                           | string   | ''              |
