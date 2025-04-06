// Inisialisasi Aplikasi
class TokoOnline {
    constructor() {
        this.initTheme();
        this.initCart();
        this.loadProducts();
        this.bindEvents();
    }
    
    // Inisialisasi tema
    initTheme() {
        const savedTheme = localStorage.getItem('theme') || 'red';
        document.documentElement.setAttribute('data-theme', savedTheme);
    }
    
    // Inisialisasi keranjang
    initCart() {
        this.cart = JSON.parse(localStorage.getItem('cart')) || [];
        this.updateCartCount();
    }
    
    // Memuat produk
    loadProducts() {
        fetch('data/products.json')
            .then(response => response.json())
            .then(products => {
                this.displayProducts(products);
            });
    }
    
    // Menampilkan produk
    displayProducts(products) {
        const container = document.querySelector('.products-grid');
        container.innerHTML = '';
        
        products.slice(0, 8).forEach(product => {
            container.innerHTML += `
                <div class="product-card" data-aos="fade-up">
                    <div class="product-image">
                        <img src="assets/images/products/${product.image}" alt="${product.name}">
                        ${product.discount ? `<div class="product-badge">-${product.discount}%</div>` : ''}
                    </div>
                    <div class="product-info">
                        <h3 class="product-title">${product.name}</h3>
                        <div class="product-price">
                            Rp ${this.formatPrice(product.price - (product.price * (product.discount || 0) / 100)}
                            ${product.discount ? `<span class="old-price">Rp ${this.formatPrice(product.price)}</span>` : ''}
                        </div>
                        <button class="add-to-cart" data-id="${product.id}">+ Keranjang</button>
                    </div>
                </div>
            `;
        });
    }
    
    // Format harga
    formatPrice(price) {
        return price.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ".");
    }
    
    // Update jumlah keranjang
    updateCartCount() {
        const count = this.cart.reduce((total, item) => total + item.quantity, 0);
        document.querySelectorAll('.cart-count').forEach(el => {
            el.textContent = count;
        });
    }
    
    // Tambah ke keranjang
    addToCart(productId) {
        // Implementasi logika keranjang
        this.updateCartCount();
    }
    
    // Binding events
    bindEvents() {
        // Theme switcher
        document.querySelectorAll('.theme-switcher').forEach(button => {
            button.addEventListener('click', () => {
                const theme = button.dataset.theme;
                document.documentElement.setAttribute('data-theme', theme);
                localStorage.setItem('theme', theme);
            });
        });
        
        // Add to cart buttons
        document.addEventListener('click', e => {
            if (e.target.classList.contains('add-to-cart')) {
                this.addToCart(e.target.dataset.id);
            }
        });
    }
}

// Jalankan aplikasi saat DOM siap
document.addEventListener('DOMContentLoaded', () => {
    new TokoOnline();
});
