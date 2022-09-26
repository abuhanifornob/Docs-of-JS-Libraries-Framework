# React Using Method And Example

### 🔭 What is React?
- 
### 👯 Why use React?
- 
###  🤔 How to Use?

List of React:

- [Programing Hero Note](#programingHeroNote)
- [searchItems](#searchItems)
- [conditionalRendering](#conditionalRendering)
- [contextApi](#contextApi)
- [handleAddtoCart](#handleAddtoCart)
- [handleRemoveFromCart](#handleRemoveFromCart)
- [customHooks](#customHooks)
- [ChildrenChange](#ChildrenChange)
- [useState](#useState)
- [useEffect](#useEffect)
- [Immutable](#Immutable)
- [searchItem](#searchItem)
- [localStorageSessionStorage](#localStorageSessionStorage)

- [Table](#Table)

### programingHeroNote
<details>
<summary>
<h4> Programing Heros All Nots</h4>
</summary:
<br >
- Note is
</details>
  
 ```js
  //................... Module 42.............................
  // Main 4 Concept ------1.Component 2.Templete 3.State 4. Routing.
  //.... We get Componet Identyfy 4 Way..
    //1.Similar in Look Differnce in data
    // 2.Container Component
    // 3. No Pattren But breakdown for working purpose
    // 4.Stated Alone Component
 // ......API To HTML Convert..........................
const loadCountries = () => {
    fetch('https://restcountries.com/v3.1/all')
        .then(response => response.json())
        .then(data => displayCountries(data));
}

const displayCountries = (countries) => {

    const countriesHTML = countries.map(country => converCountryDataToHtmlData(country));
    const container = document.getElementById('countriesID');
    console.log(container);
    console.log(countriesHTML);
    container.innerHTML = countriesHTML.join(" ");


}

const converCountryDataToHtmlData = country => {    // parametars Destructure ({name,flags}).
      const {name,flags}=country;   // Explore destructuring and send data to html elements using props(Object Propertis Mens Props)
    return `
       <div class="coun">
       
// orginal Object chaine
<!--        <h3>${country.name.common}</h3>
       <img src="${country.flags.png}"> -->
 //...................... Use Destucturing ....
         <h3>${name.common}</h3>
       <img src="${flags.png}">
        
       </div>
    `
}

loadCountries();
 //
 /* ........ benefits of What is Single Page Application (SPA)
         1.Quick Loading Time
         2.Seamless User Experience
         3.Ease in Building Feature-rich Apps
         4.Uses Less Bandwidth
   .....    disadvantages................
         1. Doesn’t Perform Well With SEO
         2.Uses a Lot of Browser Resources
         3. Security Issues
         */
//..........................Module 47.....................................................
import React, { useEffect, useState } from 'react';
import { addCardLocatStorage, removeCardLocatStorage } from '../../utilities/addCardLocalStorage';
import { getTotal } from '../../utilities/calculation';
import './Products.css'

const Products = () => {
    
    const [products,setProducts]=useState([]);  // useState Setup
    useEffect(()=>{  //     Date Face 
        fetch('products.json')
        .then(res=>res.json())
        .then(data=>setProducts(data))
    },[]);

    // Object Sumition.....
     const totalPrice=getTotal(products);
   
    return (
        <div className='products'>
            <h1>This is products Blog</h1>
            <p>Total Price is: {totalPrice}</p>
            {
                products.map(product=><DisplayProduct products={product} key={product.id}></DisplayProduct>)
            }
        </div>
    );
};

const DisplayProduct=(props)=>{
    const{name,price,id}=props.products;
    const addCard=(id)=>{
        addCardLocatStorage(id);
    }
    const removeCard=(id)=>{
           removeCardLocatStorage(id);
    }

   
    return (
        <div className='products'>
            <h2>Product Name:{name}</h2>
            <h3>Product Price:$ {price}</h3>
            <p><small>Product id:{id} </small></p>
            {/* ................. Function Aall With parametter................ */}
            <button onClick={()=>addCard(id)}>Add Card</button>  
            <button onClick={()=>removeCard(id)}> Remove Card</button>
        </div>
    )
}


export default Products;

// ...................................... utility Section................................
// lolcat Storage Date Store and Remove.......................
const addCardLocatStorage = (id) => {

        let shoppingCart = {};
        const storedCard = localStorage.getItem('shopping-cart');
        if (storedCard) {
            shoppingCart = JSON.parse(storedCard);
        }

        const quantity = shoppingCart[id];
        if (quantity) {
            const newQuantity = quantity + 1;
            shoppingCart[id] = newQuantity;

        } else {
            shoppingCart[id] = 1;
        }
        localStorage.setItem('shopping-cart', JSON.stringify(shoppingCart));


    }
    // Remove  Card Item form Local Storage....
const removeCardLocatStorage = (id) => {

    const storedCard = localStorage.getItem('shopping-cart');
    if (storedCard) {
        const storedCartParse = JSON.parse(storedCard);
        console.log(storedCartParse);
        if (id in storedCartParse) {
            delete storedCartParse[id];
            console.log(storedCartParse)
            localStorage.setItem('shopping-cart', JSON.stringify(storedCartParse));
        }
    }
}

export { addCardLocatStorage, removeCardLocatStorage }
//............................Reduce Method..................................
// const testArray = [50, 100, 50, 100, 30];
// const reduceSum = (previus, current) => previus + current;
// const getToal = testArray.reduce(reduceSum, 0)
// console.log(getToal);



const getProductsSum = (products) => {
    const reduseSum = (previus, current) => (previus + current.price);
    const productSum = products.reduce(reduseSum, 0);
    return productSum;
}

export { getProductsSum as getTotal };
  
  
  
  
 ```

### searchItems
<details>
<summary>
  <h4>What is searchItems?</h4>
</summary>
<br >
- searchItems is
</details>

```js
//step 1 
//create input field and add event handeler
const handleSearchChange = (event) => {
    console.log(event.target.value)
};
<input onChange={handleSearchChange} type="search" placeholder="Search Mockups"/>
//step 2
//set useState
const [searchResult, setSearchResult] = useState([]);
 const handleSearchChange = (event) => {
      const searchText = (event.target.value);
      console.log(searchText)

      const match = tShirts.filter(tShirt => tShirt.name.includes(searchText))
      console.log(match)
      setSearchResult(match)
  };
  
  
  // full example
     const [searchText, setSearchText] = useState([]);
    const [searchResult, setSearchResult] = useState([]);
   
    useEffect(() => {
        console.log('inside the use effect')
        fetch('tShirts.json')
        .then(res => res.json())
        .then(data => {
            const match = data.filter(d => d.name.includes(searchText));
            setSearchResult(match)
        })
    }, [searchText])

    const handleSearchChange = (event) => {
        setSearchText(event.target.value);
    };

```

### conditionalRendering
<details>
<summary>
  <h4>What is conditionalRendering?</h4>
</summary>
<br >
- conditionalRendering is
</details>

```js
//step 1 
Conditional Rendering Options
1. Element Variable
let command;
if(cart.length === 0){
    command= <p>Please Add some items</p>
}else{
    command = <p>Thanks for adding item</p>
}
2. Ternary Operator (condition ? true : false)
3. true && condition (আগের condition true হইলে পরেরটা হবে)
4. false || condition (আগের condition false হইলে পরেরটা হবে)

```

### contextApi
<details>
<summary>
  <h4>What is contextApi?</h4>
</summary>
<br >
- contextApi is . Context api using langguage changing, theme color changing.
</details>

```js
### Context Api
1. call createContext with a default getValue
2. set a variable of the context with uppercase
3. make sure you export the context to use it in other places
4. wrap you child context useing DemoContext.Provider
5. Provide a getValue
6. to consume the context from child Component
7. useContext hook and will you need to pass the contextName
====================
//step 1 
export const DemoContext = createContext('diamond');
// function er উপরে
const DemoContext = createContext('diamond');
//step 2
 const ornament = 'ring';
<DemoContext.Provider value={ornament}>
      <div>
          <h2>Grandpa</h2>
      </div>
  </DemoContext.Provider>
  // step 3 using
  import React, { useContext } from 'react';
  const ring = useContext(DemoContext);
  <p>{ring}</p>

```

### handleAddtoCart
<details>
<summary>
  <h4>What is customHooks?</h4>
</summary>
<br >
- customHooks is
</details>

```js
//step 1 
const [cart, setCart] = useState([]);

    const handleAddtoCart = (selectedItem) => {
       const newCart = [...cart, selectedItem]
        setCart(newCart)
    };
    
    // যেই cart selet korso oi ta ase ki na check koro
    const handleAddtoCart = (selectedItem) => {
        const exists = cart.find(tShirt => tShirt._id === selectedItem._id);
        if (!exists) {
            const newCart = [...cart, selectedItem]
            setCart(newCart)
        }else{
            alert('item already added')
        }
    };
// step 2  
<Cart
  cart={cart}
/>
// step 3
// distucture
{ tShirt, handleAddtoCart }
<button onClick={() => handleAddtoCart(tShirt)}>Add to Cart</button>
```

### handleRemoveFromCart
<details>
<summary>
  <h4>What is handleRemoveFromCart?</h4>
</summary>
<br >
- handleRemoveFromCart is
</details>

```js
//step 1 
const [cart, setCart] = useState([]);
const handleRemoveFromCart = (selectedItem) => {
      const rest = cart.filter(tShirt => tShirt._id !== selectedItem._id);
      setCart(rest)
  };
// step 2  
<Cart
  cart={cart}
  handleRemoveFromCart={handleRemoveFromCart}
/>
// step 3
// distucture
{cart, handleRemoveFromCart}
 <button onClick={() => handleRemoveFromCart(tShirt)}>X</button>
```

### customHooks
<details>
<summary>
  <h4>What is customHooks?</h4>
</summary>
<br >
- customHooks is
</details>

```js
//step 1 create component and file
import { useEffect, useState } from "react";

const useProducts = () => {
    const [products, setProducts] = useState([]);

    useEffect(() => {
        fetch('products.json')
        .then(res => res.json())
        .then(data => setProducts(data))
        
    }, [])
    // step 2 return your need 
    return [products, setProducts];

};
// step 3 export function
export default useProducts;

```
### ChildrenChange
<details>
<summary>
  <h4>What is ChildrenChange?</h4>
</summary>
<br >
- ChildrenChange is
</details>

```js
//step 1 create component and file
// shop component
  <div className="cart-container">
      <Cart cart={cart}>
      //child route and button change 
          <Link to='/orders'>
              <button className='btn'>Review Order</button>
          </Link>
      </Cart>
  </div>
  //step 2 create component and file
  // order component
  <Cart cart={cart}>
   //child route and button change 
        <Link to='/inventory'>
            <button className='btn'>Proceed Checkout</button>
        </Link>
        // if do not use link then use just button then using
        import { Link, useNavigate } from 'react-router-dom';
        
        const navigate = useNavigate();
        
        <button onClick={() => navigate('/inventory')} className='btn'>Proceed Checkout</button>
    </Cart>
    
    //step 3 destructure
    const Cart = ({ children }) => {
          return (
              <div className="cart">
              //step 4 using
                  {children}
              </div>
          );
    };

```

### useState
<details>
<summary>
  <h4>What is useState?</h4>
</summary>
<br >
- useState is
</details>

```js
// import
import React, { useState } from 'react';

const Example = () => {
  // Declare a new state variable, which we'll call "count"
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>
        Click me
      </button>
    </div>
  );
}

```

### useEffect
<details>
<summary>
  <h4>What is useEffect?</h4>
</summary>
<br >
- useEffect is
</details>

```js
// import
import React, {useState, useEffect } from 'react';

const Example = () => {
const [count, setCount] = useState(0);
  // Example
  useEffect(() => {
  // Update the document title using the browser API
      document.title = `You clicked ${count} times`;
  // fetch
    fetch('')
      .then(res => res.json())
      .then(data => console.log(data))
  }, [])

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>
        Click me
      </button>
    </div>
  );
}
```
### Immutable
<details>
<summary>
  <h4>What is Immutable?</h4>
</summary>
<br >
- useState is
</details>

```js
const [cart, setCart] = useState([]);

    const handleAddToCart = (product) => {
        //simple array push
        //cart.push(push)
        //array copy and new array create
        const newCart = [...cart, product];
        setCart(newCart)
    }
```
### searchItem
<details>
<summary>
  <h4>What is searchItem?</h4>
</summary>
<br >
- searchItem is
</details>

```js
  //step 1
    // create input filed and button
    <input onChange={searchFood} type="text" placeholder="Type here"/>
  //step 2
    // target input value
    const searchFood = (event) => {
        setSearchText(event.target.value)
  };
  //step 3
    //keep data
    const [searchText, setSearchText] = useState('');
    const [loadMeals, setLoadMeals] = useState([]);
  
  //step 4
  // call search api and daynamic
     //search api call
    useEffect(() => {
        const url = `https://www.themealdb.com/api/json/v1/1/search.php?s=${searchText}`;
        fetch(url)
            .then(res => res.json())
            .then(data => setLoadMeals(data.meals))
    }, [searchText])
  
  //step 5
    // map single items
      {
        loadMeals.map(loadMeal =>
                <div key={loadMeal.idMeal} className="single-meal card w-auto bg-base-100 shadow-xl">
                <figure className="">
                    <img src={loadMeal.strMealThumb} alt="Shoes" className="rounded-md" />
                </figure>
                <div className="card- p-4 items-center text-center">
                    <h2 className="card-title block  py-4 text-center">{loadMeal.strMeal}</h2>
                    <p>{loadMeal.strInstructions.slice(0, 100)}</p>
                    <div className="card-actions block py-3">
                        <button onClick={() => handleAddToOrder(loadMeal.meal)}>Order Now</button>
                    </div>
                </div>
            </div>
        )
      }
```


### localStorageSessionStorage
<details>
<summary>
  <h4>What is localStorage and SessionStorage?</h4>
</summary>
<br >
- 
</details>

```js
const Cosmetic = ({ cosmetic }) => {
    const { name, price, _id } = cosmetic;
    
    //use only one(advance, simple)
    //simple use localStorage
    const addToCart = (_id) => {
        // addToDb(_id)
        const quantity = localStorage.getItem(_id);
        if (quantity) {
            console.log('already exists')
            const newQuantity = parseInt(quantity) + 1;

            localStorage.setItem(_id, newQuantity)

        } else {
            console.log('new item')

            localStorage.setItem(_id, 1)
        }
    };
    
    // advance use LocalStorage
      const addToCart = (_id) => {
        // addToDb(_id)
        let shoppingCart;
        //get the shopping cart from local storage
        const storedCart = localStorage.getItem('shopping-cart');
        if (storedCart) {
            shoppingCart = JSON.parse(storedCart)

        } else {
            shoppingCart = {}
        }
        //add quantity
        const quantity = shoppingCart[_id];
        if (quantity) {

            const newQuantity = quantity + 1;
            shoppingCart[_id] = newQuantity;

        } else {
            shoppingCart[_id] = 1;
        }
        localStorage.setItem('shopping-cart', JSON.stringify(shoppingCart))
    };
    
      const removeFromCart = (_id) => {
        console.log('removing', _id)
        
    }

    return (
        <div className='product'>
            <h2>Buy this: {name}</h2>
            <h4>Only for: $ {price}</h4>
            <h5>Id : {_id}</h5>
            <button onClick={() => addToCart(_id)} >Add to Cart</button>
        </div>
    );
};
```

### Table
<div class="overflow-x-auto">
  <table class="table w-full">
    <!-- head -->
    <thead>
      <tr>
        <th></th>
        <th>Questions</th>
        <th>Answer</th>
      </tr>
    </thead>
    <tbody>
      <!-- row 1 -->
      <tr>
        <th>1</th>
        <td>setCount(count + 1)</td>
        <td>asynchronous</td>
      </tr>
      <!-- row 2 -->
      <tr>
        <th>2</th>
        <td>props</td>
        <td>React a uopr theke eventhandler k  props akare data pathano jai, down theke up pathano jai na. r jodi pathate hoi tahole jai jaiga jabe seijaiga evnthandler dita hobe</td>
      </tr>
      <!-- row 3 -->
      <tr>
        <th>3</th>
        <td>Uncaught TypeError: cart is not iterable</td>
        <td>looping problem</td>
      </tr>
       <!-- row 3 -->
      <tr>
        <th>3</th>
        <td>Use Short Title</td>
        <td><p className='product-name' title={name}>
            {name.length > 20 ? name.slice(0, 20) + '...' : name}
        </p></td>
      </tr>
    </tbody>
  </table>
</div>



## 🌐 Socials: Connect with Emon Hossain!

[![Facebook Badge](https://img.shields.io/badge/Facebook-1877F2?style=for-the-badge&logo=facebook&logoColor=white)](https://fb.com/emonhossain6) [![Linkedin Badge](https://img.shields.io/badge/LinkedIn-0077B5?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/emon007iu/) [![Twitter Badge](https://img.shields.io/badge/Twitter-1DA1F2?style=for-the-badge&logo=twitter&logoColor=white)](https://twitter.com/@emon_hossain7) [![Mail Badge](https://img.shields.io/badge/Gmail-D14836?style=for-the-badge&logo=gmail&logoColor=white)](mailto:emon.hossain.wd@gmail.com)

<h4>❤️🤔 You can follow my Github and other social accounts 🤔❤️</h4>
<h2>❤️ Thank you very much! ❤️</h2>
