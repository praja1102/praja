App.js

import React, { useState } from "react";
import "./App.css";
const productsData = [
  { id: 1, name: "iPhone 15", category: "Electronics", image: "https://store.storeimages.cdn-apple.com/4982/as-images.apple.com/is/iphone-15-pro-max-green-select?wid=940&hei=1112&fmt=png-alpha" },
  { id: 2, name: "Samsung Galaxy S23", category: "Electronics", image: "https://images.samsung.com/is/image/samsung/p6pim/in/sm-s911bzgmein/gallery/in-galaxy-s23-ultra-s911-449092-sm-s911bzgmein-530640054?$720_576_PNG$" },
  { id: 3, name: "T-Shirt", category: "Clothing", image: "https://cdn.pixabay.com/photo/2016/03/31/20/11/t-shirt-1299110_1280.png" },
  { id: 4, name: "Jeans", category: "Clothing", image: "https://cdn.pixabay.com/photo/2016/03/31/19/58/jeans-1299108_1280.png" },
  { id: 5, name: "Shoes", category: "Footwear", image: "https://cdn.pixabay.com/photo/2016/12/06/18/27/shoes-1886347_1280.png" },
  { id: 6, name: "Bluetooth Speaker", category: "Electronics", image: "https://cdn.pixabay.com/photo/2017/03/24/18/48/speaker-2178465_1280.png" },
  { id: 7, name: "Laptop", category: "Electronics", image: "https://cdn.pixabay.com/photo/2014/05/02/21/50/laptop-336704_1280.png" },
  { id: 8, name: "Smartwatch", category: "Electronics", image: "https://cdn.pixabay.com/photo/2017/03/24/19/44/smartwatch-2181160_1280.png" },
  { id: 9, name: "Earbuds", category: "Electronics", image: "https://cdn.pixabay.com/photo/2016/11/22/19/09/earphone-1851243_1280.png" },
  { id: 10, name: "Tablet", category: "Electronics", image: "https://cdn.pixabay.com/photo/2016/11/29/04/13/ipad-1867760_1280.png" }
];
function App() {
  const [selectedCategory, setSelectedCategory] = useState("All");
  const [searchTerm, setSearchTerm] = useState("");

  const categories = ["All", ...new Set(productsData.map(product => product.category))];

  const filteredProducts = productsData.filter(product => {
    const matchesCategory = selectedCategory === "All" || product.category === selectedCategory;
    const matchesSearch = product.name.toLowerCase().includes(searchTerm.toLowerCase());
    return matchesCategory && matchesSearch;
  });
  return (
    <div className="App">
      <h1>Product Catalog</h1>

      {/* Search Box */}
      <input
        type="text"
        placeholder="Search products..."
        value={searchTerm}
        onChange={(e) => setSearchTerm(e.target.value)}
        className="search-box"
      />

      {/* Category Filters */}
      <div className="filters">
        {categories.map((cat, index) => (
          <button
            key={index}
            onClick={() => setSelectedCategory(cat)}
            className={selectedCategory === cat ? "active" : ""}
          >
            {cat}
          </button>
        ))}
      </div>

      {/* Product Grid */}
      <div className="product-grid">
        {filteredProducts.length > 0 ? (
          filteredProducts.map(product => (
            <div className="product-card" key={product.id}>
              <img src={product.image} alt={product.name} />
              <h3>{product.name}</h3>
              <p>{product.category}</p>
            </div>
          ))
        ) : (
          <p>No products found.</p>
        )}
      </div>
    </div>
  );
}

App.css
.App {
  text-align: center;
  font-family: Arial, sans-serif;
  padding: 20px;
  background-color: #f9f9f9;
}

h1 {
  color: #1E90FF;
}

.search-box {
  padding: 10px;
  width: 250px;
  margin-bottom: 20px;
  border-radius: 8px;
  border: 1px solid #ccc;
}

.filters {
  margin-bottom: 20px;
}

.filters button {
  margin: 5px;
  padding: 10px 15px;
  border: none;
  border-radius: 8px;
  background-color: #f0f0f0;
  cursor: pointer;
  transition: 0.3s;
}

.filters button:hover {
  background-color: #1E90FF;
  color: white;
}

.filters button.active {
  background-color: #1E90FF;
  color: white;
}

.product-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(180px, 1fr));
  gap: 20px;
}

.product-card {
  border: 1px solid #ddd;
  border-radius: 10px;
  padding: 10px;
  background-color: white;
  transition: 0.3s;
}

.product-card:hover {
  transform: scale(1.05);
  box-shadow: 0 5px 15px rgba(0,0,0,0.2);
}

.product-card img {
  width: 100%;
  height: 150px;
  object-fit: contain;
  border-radius: 10px;
}


export default App;

