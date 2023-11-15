## 오늘 공부한 내용 ✏

### singleton pattern

DI가 싱글톤 패턴인가? X 

밖에서 의존성 주입해서 생성자 한번으로 모든 곳에서 재사용

```jsx
// product.controller.js

import { CashService } from "./services/cash.service.js";
import { ProductService } from "./services/product.service.js";

export class ProductController {
  buyProduct = (req, res) => {
    // 1. 가진돈 검증하는 코드 (10줄 => 2줄)
    const cashService = new CashService();
    const hasMoney = cashService.checkValue(); // true 또는 false 리턴

    // 2. 판매여부 검증하는 코드 (10줄 => 2줄)
    const productService = new ProductService();
    const isSoldout = productService.checkSoldout(); // true 또는 false 리턴

    // 3. 상품 구매하는 코드
    if (hasMoney && !isSoldout) {
      res.send("상품 구매 완료!!");
    }
  };

  refundProduct = (req, res) => {
    // 1. 판매여부 검증하는 코드 (대략 10줄 정도)
    const productService = new ProductService();
    const isSoldout = productService.checkSoldout(); // true 또는 false 리턴

    // 2. 상품 환불하는 코드
    if (isSoldout) {
      res.send("상품 환불 완료!!");
    }
  };
}
```

```jsx
// coupon.controller.js

import { CashService } from "./services/cash.service.js";

export class CouponController {
  buyCoupon = (req, res) => {
    // 1. 가진돈 검증하는 코드 (10줄 => 2줄)
    const cashService = new CashService();
    const hasMoney = cashService.checkValue(); // true 또는 false 리턴

    // 2. 쿠폰 구매하는 코드
    if (hasMoney) {
      res.send("쿠폰 구매 완료!!");
    }
  };
}
```

```jsx
// index.js

import express from "express";
import { ProductController } from "./mvc/controllers/product.controller.js";
import { CouponController } from "./mvc/controllers/coupon.controller.js";
import { ProductService } from "./mvc/controllers/services/product.service.js";

const app = express();

// 추가되는 부분
const cashService = new CashService();

// 상품 API
const productController = new ProductController(cashService);
app.post("/products/buy", productController.buyProduct);
app.post("/products/refund", productController.refundProduct);

// 쿠폰 API
const couponController = new CouponController();
app.post("/coupons/buy", couponController.buyCoupon);

app.listen(3000);
```

```jsx
// product.controller.js

// import { ProductService } from './services/product.service.js'
import { CashService } from "./services/point.service.js";

export class ProductController {
  constructor(moneyService) {
    this.moneyService = moneyService;
  }

  buyProduct = (req, res) => {
    // 1. 가진돈 검증하는 코드(10줄 => 2줄)
    // const cashService = new CashService();
    const hasMoney = this.moneyService.checkValue();

    // 판매여부 검증하는 코드(10줄 => 2줄)
    const productService = new ProductService()
    const isSoldout = this.productService.checkSoldout();

    // 3. 상품 구매하는 코드
    if (hasMoney && !isSoldout) {
      res.send("상품 구매 완료!!");
    }
  };

  refundProduct = (req, res) => {
    // 1. 판매여부 검증하는 코드(10줄 => 2줄)
    // const productService = new ProductService()
    const isSoldout = this.productService.checkSoldout();

    // 2. 상품 환불하는 코드
    if (isSoldout) {
      res.send("상품 환불 완료!!");
    }
  };
}
```

## 어려웠던 내용 ⚔

## 궁금한내용 / 부족한 내용 🛡

## 느낀점 🎯

## 오늘 참고한 자료 📚

[https://poiemaweb.com/js-this](https://poiemaweb.com/js-this)
