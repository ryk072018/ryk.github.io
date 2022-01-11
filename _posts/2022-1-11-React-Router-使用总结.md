# React-Router使用总结

#### 1.下载 React Router

```jsx
npm install react-router-dom@6
```

#### 2.连接URL：将应用程序连接到 浏览器的 URL。使用 `BrowserRouter`

```jsx
# main.jsx
import { render } from 'react-dom'
import { BrowserRouter } from 'react-router-dom'
import App from './App'

const rootElement = document.getElementById('root')
render(
    <BrowserRouter>
    	<App />
    </BrowserRouter>,
    rootElement
)
```

#### 3.添加 `Link` 导航 

```jsx
# app.jsx
import { Link } from 'react-router-dom'

export default function App() {
    return(
    	<div>
            <h1>Book</h1>
            <nav>
            	<Link to="/invoices">Invoices</Link>
                <Link to="/expense">Expense</Link>
            </nav>
        </div>
    )
}
```

#### 4.创建一个 `Route Config`。 使用嵌套路由。在 父路由 中嵌套 两个子路由。

```jsx
#main.jsx
import { render } from 'react-dom'
import { 
    BrowserRouter,
    Routes,
    Route
       } from 'react-router-dom'
import App from './App'
import Expenses from './router/expenses'
import Invoices from './router/invoices'

const rootElement = document.getElementById('root')
render{
    <BrowserRouter>
        <Routes>
        	<Route path='/' element={<App />}>
            	<Route path='expenses' element={<Expenses />} />
            	<Route path='invoices' element={<Invoices />} />
            </Route>
        </Routes>
    </BrowserRouter>,
    rootElement
}

```

#### 使用 `Link` 导航，使用 `Outlet` 作为子路由的出口渲染子组件

```jsx
#app.jsx
import { Outlet, Link } from 'react-router-dom'

export default function App() {
    return(
    	<div>
        	<nav>
            	<Link to="/invoices">Invoices</Link>
                <Link to="/expenses">Expenses</Link>
            </nav>
            <Outlet />
        </div>
    )
}
```

#### 总结1：`<Link to={} />` 路径中有变量时 用 反引号 

```jsx
<Link to={`/invoices/${invoice.number}`}>例子1</Link>
```

#### 5.使用 `useParams` 获取 `URL` 中的参数

```jsx
#main.jsx
<Route path="invoices" element={<Invoices />}>
	<Route path=":invoiceId" element={<Invoice />}>
</Route>
```

```jsx
#invoice.jsx
import { useParams } from 'react-router-dom'

export default function Invoices() {
    let params = useParams()
    return(
        <h2>{params.invoiceId}</h2>
    )
}
```

##### 注意：`params` 的 `key` 和路由路径中的动态段一致

```jsx
:invoiceId -> params.invoiceId
```

#### 6.index 路由

```jsx
<Route index element={} />
```

#### 7.活动链接 使用 `NavLink` 实现

```jsx
<NavLink className='red'/>

// function
<NavLink className={({ isActive }) => isActive ? 'red' : 'blue' }/>
```

#### 8.搜索参数 使用 `useSearchParams` 实现

```jsx
import { useSearchParams } from 'react-router-dom'

export default function Invoices() {
	let [searchParams, setSearchParams] = useSearchParams()

    return(
        <div>
        	<input 
                value={searchParams.get('filter') || ''} 
                onChange={(event) => {
                    let filter = event.target.value
                    if(filter){
                        setSearchParams({ filter })
                    }else{
                        setSearchParams({})
                    }
                }}
             />
        </div>
    )
}
```

- ##### `setSearchParams()` 把 `?filter=...` 搜索参数放到URL 并重新呈现路由器

#### 9.以编程方式导航 使用 `vueNavigate()`

```jsx
import { useNavigate} from 'react-router-dom'

export default function Invoice() {
    let navigate = useNavigate()
    return(
    	<button onClick={() => {
                navigate('/invoices')
            }}>
            返回
        </button>
    )
}
```

