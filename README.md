# MaasNeer-
Hay MaasNeer uger

import { ShoppingCart, Search, Menu, User, Heart, Star } from 'lucide-react';
import { useState } from 'react';
import { useNavigate } from 'react-router-dom';
import { Button } from '@/components/ui/button';
import { Input } from '@/components/ui/input';
import { Card, CardContent } from '@/components/ui/card';
import { Badge } from '@/components/ui/badge';

const Index = () => {
  const navigate = useNavigate();
  const [cartItems, setCartItems] = useState(0);
  const [searchQuery, setSearchQuery] = useState('');

  const categories = [
    'Electronics', 'Fashion', 'Home & Garden', 'Sports', 'Books', 'Health', 'Toys', 'Automotive'
  ];

  const featuredProducts = [
    {
      id: 1,
      name: "Wireless Bluetooth Headphones",
      price: 79.99,
      originalPrice: 99.99,
      rating: 4.5,
      reviews: 2543,
      image: "https://images.unsplash.com/photo-1505740420928-5e560c06d30e?w=300&h=300&fit=crop",
      badge: "Best Seller"
    },
    {
      id: 2,
      name: "Smart Fitness Watch",
      price: 199.99,
      originalPrice: 249.99,
      rating: 4.7,
      reviews: 1876,
      image: "https://images.unsplash.com/photo-1523275335684-37898b6baf30?w=300&h=300&fit=crop",
      badge: "Limited Deal"
    },
    {
      id: 3,
      name: "Portable Laptop Stand",
      price: 34.99,
      originalPrice: 49.99,
      rating: 4.3,
      reviews: 892,
      image: "https://images.unsplash.com/photo-1527864550417-7fd91fc51a46?w=300&h=300&fit=crop",
      badge: "Choice"
    },
    {
      id: 4,
      name: "Wireless Charging Pad",
      price: 24.99,
      originalPrice: 34.99,
      rating: 4.2,
      reviews: 1245,
      image: "https://images.unsplash.com/photo-1609091839311-d5365f9ff1c5?w=300&h=300&fit=crop",
      badge: "Deal"
    }
  ];

  const addToCart = (productId: number) => {
    setCartItems(prev => prev + 1);
  };

  const renderStars = (rating: number) => {
    return Array.from({ length: 5 }, (_, i) => (
      <Star
        key={i}
        className={`w-4 h-4 ${i < Math.floor(rating) ? 'fill-yellow-400 text-yellow-400' : 'text-gray-300'}`}
      />
    ));
  };

  return (
    <div className="min-h-screen bg-gray-50">
      {/* Header */}
      <header className="bg-slate-900 text-white sticky top-0 z-50">
        <div className="container mx-auto px-4">
          {/* Top Header */}
          <div className="flex items-center justify-between py-2 border-b border-slate-700">
            <div className="flex items-center space-x-6">
              <h1 className="text-2xl font-bold text-orange-400">AmazonLike</h1>
              <div className="hidden md:flex items-center space-x-4 text-sm">
                <span>Deliver to New York 10001</span>
              </div>
            </div>
            <div className="flex items-center space-x-4">
              <span className="text-sm">Hello, Sign in</span>
              <Button 
                variant="ghost" 
                size="sm" 
                className="text-white hover:text-orange-400"
                onClick={() => navigate('/account')}
              >
                <User className="w-4 h-4 mr-1" />
                Account
              </Button>
            </div>
          </div>

          {/* Main Header */}
          <div className="flex items-center py-2 space-x-4">
            <Button variant="ghost" size="sm" className="text-white hover:text-orange-400 md:hidden">
              <Menu className="w-5 h-5" />
            </Button>
            
            {/* Search Bar */}
            <div className="flex-1 max-w-2xl">
              <div className="relative flex">
                <Input
                  type="text"
                  placeholder="Search products..."
                  value={searchQuery}
                  onChange={(e) => setSearchQuery(e.target.value)}
                  className="rounded-r-none border-r-0 focus:ring-orange-400 focus:border-orange-400"
                />
                <Button className="rounded-l-none bg-orange-400 hover:bg-orange-500 text-slate-900">
                  <Search className="w-4 h-4" />
                </Button>
              </div>
            </div>

            <div className="flex items-center space-x-4">
              <Button variant="ghost" size="sm" className="text-white hover:text-orange-400 relative">
                <Heart className="w-5 h-5" />
                <span className="hidden sm:inline ml-1">Wishlist</span>
              </Button>
              <Button variant="ghost" size="sm" className="text-white hover:text-orange-400 relative">
                <ShoppingCart className="w-5 h-5" />
                <span className="hidden sm:inline ml-1">Cart</span>
                {cartItems > 0 && (
                  <Badge className="absolute -top-2 -right-2 bg-orange-400 text-slate-900 text-xs">
                    {cartItems}
                  </Badge>
                )}
              </Button>
            </div>
          </div>

          {/* Navigation */}
          <nav className="hidden md:flex items-center space-x-6 py-2 text-sm">
            <Button variant="ghost" size="sm" className="text-white hover:text-orange-400">
              <Menu className="w-4 h-4 mr-1" />
              All
            </Button>
            {categories.map((category) => (
              <Button key={category} variant="ghost" size="sm" className="text-white hover:text-orange-400">
                {category}
              </Button>
            ))}
          </nav>
        </div>
      </header>

      {/* Hero Section */}
      <section className="bg-gradient-to-r from-blue-600 to-purple-700 text-white py-12">
        <div className="container mx-auto px-4 text-center">
          <h2 className="text-4xl font-bold mb-4">Great Deals Every Day</h2>
          <p className="text-xl mb-6">Discover millions of products at unbeatable prices</p>
          <Button className="bg-orange-400 hover:bg-orange-500 text-slate-900 text-lg px-8 py-3">
            Shop Now
          </Button>
        </div>
      </section>

      {/* Categories Grid */}
      <section className="py-8 bg-white">
        <div className="container mx-auto px-4">
          <h3 className="text-2xl font-bold mb-6">Shop by Category</h3>
          <div className="grid grid-cols-2 md:grid-cols-4 lg:grid-cols-8 gap-4">
            {categories.map((category) => (
              <Card key={category} className="hover:shadow-lg transition-shadow cursor-pointer">
                <CardContent className="p-4 text-center">
                  <div className="w-16 h-16 bg-gray-200 rounded-full mx-auto mb-2"></div>
                  <p className="text-sm font-medium">{category}</p>
                </CardContent>
              </Card>
            ))}
          </div>
        </div>
      </section>

      {/* Featured Products */}
      <section className="py-8">
        <div className="container mx-auto px-4">
          <h3 className="text-2xl font-bold mb-6">Featured Products</h3>
          <div className="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-6">
            {featuredProducts.map((product) => (
              <Card key={product.id} className="hover:shadow-lg transition-shadow">
                <CardContent className="p-4">
                  <div className="relative mb-4">
                    <img
                      src={product.image}
                      alt={product.name}
                      className="w-full h-48 object-cover rounded-lg"
                    />
                    {product.badge && (
                      <Badge className="absolute top-2 left-2 bg-orange-400 text-slate-900">
                        {product.badge}
                      </Badge>
                    )}
                    <Button
                      variant="ghost"
                      size="sm"
                      className="absolute top-2 right-2 text-gray-600 hover:text-red-500"
                    >
                      <Heart className="w-4 h-4" />
                    </Button>
                  </div>
                  
                  <h4 className="font-semibold mb-2 line-clamp-2">{product.name}</h4>
                  
                  <div className="flex items-center mb-2">
                    <div className="flex">{renderStars(product.rating)}</div>
                    <span className="text-sm text-gray-600 ml-1">({product.reviews})</span>
                  </div>
                  
                  <div className="mb-4">
                    <span className="text-lg font-bold text-red-600">${product.price}</span>
                    {product.originalPrice && (
                      <span className="text-sm text-gray-500 line-through ml-2">
                        ${product.originalPrice}
                      </span>
                    )}
                  </div>
                  
                  <Button
                    onClick={() => addToCart(product.id)}
                    className="w-full bg-orange-400 hover:bg-orange-500 text-slate-900"
                  >
                    Add to Cart
                  </Button>
                </CardContent>
              </Card>
            ))}
          </div>
        </div>
      </section>

      {/* Footer */}
      <footer className="bg-slate-900 text-white py-12">
        <div className="container mx-auto px-4">
          <div className="grid grid-cols-1 md:grid-cols-4 gap-8">
            <div>
              <h4 className="font-bold mb-4 text-orange-400">Get to Know Us</h4>
              <ul className="space-y-2 text-sm">
                <li><a href="#" className="hover:text-orange-400">About Us</a></li>
                <li><a href="#" className="hover:text-orange-400">Careers</a></li>
                <li><a href="#" className="hover:text-orange-400">Press Releases</a></li>
              </ul>
            </div>
            <div>
              <h4 className="font-bold mb-4 text-orange-400">Make Money with Us</h4>
              <ul className="space-y-2 text-sm">
                <li><a href="#" className="hover:text-orange-400">Sell on AmazonLike</a></li>
                <li><a href="#" className="hover:text-orange-400">Become an Affiliate</a></li>
                <li><a href="#" className="hover:text-orange-400">Advertise Your Products</a></li>
              </ul>
            </div>
            <div>
              <h4 className="font-bold mb-4 text-orange-400">Let Us Help You</h4>
              <ul className="space-y-2 text-sm">
                <li><a href="#" className="hover:text-orange-400">Your Account</a></li>
                <li><a href="#" className="hover:text-orange-400">Your Orders</a></li>
                <li><a href="#" className="hover:text-orange-400">Shipping Rates</a></li>
                <li><a href="#" className="hover:text-orange-400">Returns & Replacements</a></li>
                <li><a href="#" className="hover:text-orange-400">Help</a></li>
              </ul>
            </div>
            <div>
              <h4 className="font-bold mb-4 text-orange-400">Connect with Us</h4>
              <ul className="space-y-2 text-sm">
                <li><a href="#" className="hover:text-orange-400">Facebook</a></li>
                <li><a href="#" className="hover:text-orange-400">Twitter</a></li>
                <li><a href="#" className="hover:text-orange-400">Instagram</a></li>
              </ul>
            </div>
          </div>
          <div className="border-t border-slate-700 mt-8 pt-8 text-center text-sm">
            <p>&copy; 2024 AmazonLike. All rights reserved.</p>
          </div>
        </div>
      </footer>
    </div>
  );
};

export default Index;


