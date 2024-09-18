Fahadalm13
fahadalm13
Do Not Disturb
Fatimah Alabdi, Mohammed Tariq

Mohammed Tariq — 09/16/2024 11:32 AM
public void updateOrder
public void updateOrder(Order order, Integer orderId, Integer userId) {
        // Find the existing order
        Order oldOrder = orderRepository.findOrderById(orderId);
        if (oldOrder == null) {
            throw new ApiException("Order not found");
        }
Expand
message.txt
3 KB
===============
public int getDiscount(Integer userId,int totalAmount) {
        User user1 = authRepository.findUserById(userId);
        Integer totalOrdersHave=0;
        if (user1.getRole().equals("FACILITY")) {
            totalOrdersHave= orderRepository.countOrdersByFacilityId(userId);
        } 
        if (user1.getRole().equals("CUSTOMER")) {
            totalOrdersHave= orderRepository.countOrdersByCustomerId(userId);
        }

        if (totalOrdersHave>=5){
            double discount=0.3*totalAmount;
            discount=totalAmount-discount;
            return (int) discount;
        }else {
            return 0;
        }
    }
Fatimah Alabdi — 09/16/2024 1:21 PM
RecyclingRequestRepository>>>>>@Query("SELECT r.productName FROM RecyclingRequest r GROUP BY r.productName " +
            "ORDER BY COUNT(r.productName) DESC")
    List<String> findMostRecycledProducts();
FacilityService>>>>public List<String> getPopularRecycledProducts() {
        return recyclingRequestRepository.findMostRecycledProducts();
    }
controller >>@GetMapping("/popular-recycle-products")
    public ResponseEntity getPopularRecycledProducts() {
        List<String> popularProducts = facilityService.getPopularRecycledProducts();
        return ResponseEntity.status(200).body(popularProducts);
    }
Mohammed Tariq — Yesterday at 10:14 AM
<dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
            <exclusions>
                <exclusion>
                    <groupId>junit</groupId>
                    <artifactId>junit</artifactId>
                </exclusion>
            </exclusions>
        </dependency>

        <dependency>
            <groupId>org.junit.jupiter</groupId>
            <artifactId>junit-jupiter-api</artifactId>
            <scope>test</scope>
        </dependency>

        <dependency>
            <groupId>org.junit.jupiter</groupId>
            <artifactId>junit-jupiter-engine</artifactId>
            <scope>test</scope>
        </dependency>
Mohammed Tariq — Yesterday at 10:22 AM
public List<Order> getAllOrder(Integer userId) {
        // Check if there are orders for the facility
        List<Order> facilityOrders = orderRepository.findOrdersByFacilityId(userId);
        if (!facilityOrders.isEmpty()) {
            return facilityOrders;
        }

        // Check if there are orders for the customer
        List<Order> customerOrders = orderRepository.findOrdersByCustomerId(userId);
        if (!customerOrders.isEmpty()) {
            return customerOrders;
        }

        // No orders found for either facility or customer
        throw new ApiException("You don't have any orders");
    }
Fahadalm13 — Yesterday at 10:24 AM
// Delete a product
    public void deleteProduct(Integer user_id , Integer id) {
        Product product = productRepository.findProductById(id);
        if (product == null) {
            throw new ApiException("Product not found");
        }
        productRepository.delete(product);
    }
public void deleteProduct(Integer user_id , Integer id) {
        Supplier user = supplierRepository.findSupplierById(user_id);
        if (user == null) {
            throw new ApiException("Supplier not found");
        }
        Product product = productRepository.findProductById(id);
        if (product == null) {
            throw new ApiException("Product not found");
        }
        productRepository.delete(product);
    }
Mohammed Tariq — Yesterday at 10:35 AM
=====================
public void deleteProductTest() {

        when(supplierRepository.findSupplierById(supplier.getId())).thenReturn(supplier);
        when(productRepository.findProductById(product1.getId())).thenReturn(product1);

        productService.deleteProduct(supplier.getId(), product1.getId());

        verify(supplierRepository, times(1)).findSupplierById(supplier.getId());
        verify(productRepository, times(1)).findProductById(product1.getId());
        verify(productRepository, times(1)).delete(product1);
    }
==============
@Test
    public void deleteProductNoAccessTest() {
        when(supplierRepository.findSupplierById(user.getId())).thenReturn(null);


        ApiException thrown = assertThrows(ApiException.class, () -> productService.deleteProduct(user.getId(), product1.getId()));
        assertEquals("Supplier not found", thrown.getMessage());

        when(supplierRepository.findSupplierById(supplier.getId())).thenReturn(supplier);
        when(productRepository.findProductById(product1.getId())).thenReturn(null);

        thrown = assertThrows(ApiException.class, () -> productService.deleteProduct(supplier.getId(), product1.getId()));
        assertEquals("Product not found", thrown.getMessage());
    }
Fahadalm13 — Yesterday at 10:40 AM
https://github.com/FahadAlm13/FinalProjectV1.git
GitHub
GitHub - FahadAlm13/FinalProjectV1
Contribute to FahadAlm13/FinalProjectV1 development by creating an account on GitHub.
GitHub - FahadAlm13/FinalProjectV1
Fahadalm13 — Yesterday at 11:31 AM
 public SecurityFilterChain securityFilterChain(HttpSecurity http) throws Exception {
        http.csrf().disable()
                .sessionManagement()
                .sessionCreationPolicy(SessionCreationPolicy.IF_REQUIRED)
                .and()
                .authenticationProvider(daoAuthenticationProvider())
Expand
public SecurityFilterChain security.txt
4 KB
https://app.getpostman.com/join-team?invite_code=c59f913c4a2ef25fd6bad9169cee8b90&target_code=ec2db885da1106eaa9723066409f58e6
A teammate invited you to join their workspace
Join this workspace to start viewing and collaborating on API requests, collections, designs and more.
A teammate invited you to join their workspace
Mohammed Tariq — Yesterday at 11:57 AM
@PutMapping("/delete/{orderId}")
    public ResponseEntity deleteOrderById(@AuthenticationPrincipal User user, @PathVariable Integer orderId) {
        orderService.deleteOrder(orderId, user.getId());
        return ResponseEntity.status(200).body("order deleted successfully");
    }
Mohammed Tariq — Yesterday at 1:25 PM
-==================
public double getDiscount(Integer userId,double totalAmount) {
        User user1 = authRepository.findUserById(userId);
        Integer totalOrdersHave=0;
        if (user1.getRole().equals("FACILITY")) {
            totalOrdersHave= orderRepository.countOrdersByFacilityId(userId);
        }
        if (user1.getRole().equals("CUSTOMER")) {
            totalOrdersHave= orderRepository.countOrdersByCustomerId(userId);
        }

        if (totalOrdersHave>=5){
            double discount=0.3*totalAmount;
            discount=totalAmount-discount;
            return  discount;
        }else {
            return totalAmount;
        }
    }
Mohammed Tariq — Yesterday at 3:18 PM
@PutMapping("/rejected-Offer/{priceOfferId}")
    public ResponseEntity rejectOffer(@AuthenticationPrincipal User user,@PathVariable Integer priceOfferId) {
        priceOfferService.rejectedOffer(user.getId(), priceOfferId);
        return ResponseEntity.status(200).body("PriceOffer rejected successfully");

    }
================
//REJECTED OFFER
    public void rejectedOffer(Integer facilityId,Integer priceOfferId) {
        PriceOffer priceOffer =priceOfferRepository.findPriceOfferById(priceOfferId);
        if (priceOffer == null) {
            throw new ApiException("Price Offer not found");
        }

        RecyclingRequest recyclingRequest = priceOffer.getRecyclingRequest();
        if (!recyclingRequest.getFacility_recycle().getId().equals(facilityId)) {
            throw new ApiException("Facility not authorized to Rejected this offer.");
        }

        if (priceOffer.getStatus().equals("APPROVED")) {
            throw new ApiException("Price Offer already submitted for this request.");
        }
        priceOffer.setStatus("REJECTED");
        priceOfferRepository.save(priceOffer);
    }
Mohammed Tariq — Yesterday at 4:04 PM
================
public Map<String, Object> getFacilityRecycleANDRequest(Integer facilityId) {
        Facility facility = facilityRepository.findFacilityById(facilityId);

        Map<String, Object> facilityDataMap = new HashMap<>();

        facilityDataMap.put("facility_Recycle", facility.getFacility_recycle());

        Set<FacilityRequest> facilityRequests = facility.getFacilityRequests();

        facilityDataMap.put("facility_Request", facilityRequests);

        return facilityDataMap;
    }
@GetMapping("/get-recycle-request")
    public ResponseEntity recycleRequest(@AuthenticationPrincipal User user) {
        return ResponseEntity.status(200).body(facilityService.getFacilityRecycleANDRequest(user.getId()));
    }
Mohammed Tariq — Yesterday at 4:32 PM
facility model:
@OneToMany(cascade = CascadeType.ALL,mappedBy = "facility")
    private Set<Review> reviews
customer model: 
@OneToMany(cascade = CascadeType.ALL,mappedBy = "customer")
    private Set<Review> reviews;
Review model:
@ManyToOne
    @JsonIgnore
    private Customer customer;

    @ManyToOne
    @JsonIgnore
    private Facility facility;
========================================================
review service
======================
package spring.boot.fainalproject.Service;

import lombok.RequiredArgsConstructor;
import org.springframework.stereotype.Service;
import spring.boot.fainalproject.API.ApiException;
import spring.boot.fainalproject.Model.*;
Expand
message.txt
3 KB
Mohammed Tariq — Yesterday at 4:42 PM
package spring.boot.fainalproject.Controller;

import jakarta.validation.Valid;
import lombok.RequiredArgsConstructor;
import org.springframework.http.ResponseEntity;
import org.springframework.security.core.annotation.AuthenticationPrincipal;
import org.springframework.web.bind.annotation.*;
import spring.boot.fainalproject.Model.Review;
import spring.boot.fainalproject.Model.User;
import spring.boot.fainalproject.Service.ReviewService;

@RestController
@RequestMapping("/api/v1/review")
@RequiredArgsConstructor
public class ReviewController {
    private final ReviewService reviewService;

    @GetMapping("/get-all")
    public ResponseEntity getAllReviews() {
        return ResponseEntity.status(200).body(reviewService.findAllReviewsByOrderId());
    }


    @PostMapping("/add-review/{orderId}")
    public ResponseEntity addReview(@PathVariable Integer orderId, @Valid @RequestBody Review review, @AuthenticationPrincipal User user) {
        reviewService.addReviewForProduct(orderId,review, user.getId());
        return ResponseEntity.status(200).body("review added successfully");
    }

    @PutMapping("/update/{reviewId}")
    public ResponseEntity updateReview(@Valid @RequestBody Review review, @AuthenticationPrincipal User user, @PathVariable Integer reviewId) {
        reviewService.updateReviewForProduct(reviewId,review, user.getId());
        return ResponseEntity.status(200).body("update successful");
    }

    @DeleteMapping("/delete/{reviewId}/{userId}")
    public ResponseEntity deleteReview(@PathVariable Integer userId,@PathVariable Integer reviewId,@AuthenticationPrincipal User user) {
        reviewService.deleteReviewForProduct(user.getId(), reviewId,userId);
        return ResponseEntity.status(200).body("delete successful");
    }

}
==============================================================================
package spring.boot.fainalproject.Repository;

import org.springframework.data.jpa.repository.JpaRepository;
import org.springframework.data.jpa.repository.Query;
import org.springframework.stereotype.Repository;
import spring.boot.fainalproject.Model.Review;
@Repository
public interface ReviewRepository extends JpaRepository<Review, Integer> {
    Review findReviewById(Integer reviewId);

    @Query("select r from Review r where r.customer.id=?1")
    void deleteReviewByCustomerId(Integer customerId);
    @Query("select r from Review r where r.facility.id=?1")
    void deleteReviewByFacilityId(Integer facilityId);
}
package spring.boot.fainalproject.Advise;

import jakarta.validation.ConstraintViolationException;
import org.springframework.dao.DataIntegrityViolationException;
import org.springframework.dao.InvalidDataAccessResourceUsageException;
import org.springframework.http.ResponseEntity;
Expand
message.txt
4 KB
You missed a call from 
Fatimah Alabdi
 that lasted a few seconds.
 — Yesterday at 11:13 PM
Fahadalm13
 started a call that lasted 3 hours.
 — Yesterday at 11:15 PM
Mohammed Tariq — Today at 12:05 AM
@PutMapping("/update-by-userId/{orderId}")
    public ResponseEntity updateOrderById(@Valid @RequestBody Order order,@PathVariable Integer orderId, @AuthenticationPrincipal User user) {
        orderService.updateOrder(order, orderId, user.getId());
        return ResponseEntity.status(200).body(new ApiResponse("order updated successfully"));
    }
Mohammed Tariq — Today at 12:53 AM
فهد
# JumlaCycle

## Contact Information

- **Name:** Fahad Almusllam
- **Email:** [F.a.a.m900@gmail.com](mailto:F.a.a.m900@gmail.com)
Expand
message.txt
6 KB
فاطمه
# JumlaCycle

## Contact Information

- **Name:** Fatimah Alabdi
- **Email:** [fatimahalabdi22@gmail.com](mailto:fatimahalabdi22@gmail.com)
Expand
message.txt
6 KB
Fatimah Alabdi — Today at 1:24 AM
public List<PriceOffer> getAllPriceOfferMadeBySupplier(Integer userId) {
        Supplier supplier = supplierRepository.findSupplierById(userId);
        List<PriceOffer> priceOffers = priceOfferRepository.findBySupplier(supplier);
        return priceOffers;

    }
List<PriceOffer> findBySupplier(Supplier supplier);
@GetMapping("/get-my-price-offer")
    public ResponseEntity getAllPriceOfferMadeBySupplier(@AuthenticationPrincipal User user) {
        List<PriceOffer> priceOffers=supplierService.getAllPriceOfferMadeBySupplier(user.getId());
        return ResponseEntity.status(200).body(priceOffers);
    }
Mohammed Tariq — Today at 9:08 AM
=======================================================
public int getDiscount(Integer userId,int totalAmount) {
        User user1 = authRepository.findUserById(userId);
        Integer totalOrdersHave=0;
        if (user1.getRole().equals("FACILITY")) {
            totalOrdersHave= orderRepository.countOrdersByFacilityId(userId);
        }
        if (user1.getRole().equals("CUSTOMER")) {
            totalOrdersHave= orderRepository.countOrdersByCustomerId(userId);
        }

        if (totalOrdersHave>=5){
            double discount=0.3*totalAmount;
            discount=totalAmount-discount;
            return (int) discount;
        }else {
            return totalAmount;
        }
    }
Mohammed Tariq — Today at 9:23 AM
if (user.getRole().equals("CUSTOMER")||user.getRole().equals("FACILITY")) {

            // Update product quantity and manage relationships
            product.setQuantity(product.getQuantity() - order.getQuantity());
            order.getProducts().add(product);
            order.setOrderStatus("Pending");
            product.getOrders().add(order);

            // Save both order and product
            orderRepository.save(order);
            productRepository.save(product);
        }else {
            throw new ApiException("You don't have any accesses to add order");
        }
Mohammed Tariq — Today at 9:38 AM
@Query("select o from Order o where o.facility_orders=?1 and o.orderStatus=?2")
    Order findOrderByFacility_orders(Integer id,Integer ordersStatus);

    @Query("select o from Order o where o.customer_orders=?1 and o.orderStatus=?2")
    Order findOrderByCustomer_orders(Integer id,Integer ordersStatus);
Fahadalm13 — Today at 9:39 AM
"status": 500,
    "error": "Internal Server Error",
    "trace": "java.lang.NullPointerException: Cannot invoke "spring.boot.fainalproject.Model.Facility.getId()" because the return value of "spring.boot.fainalproject.Model.Order.getFacility_orders()" is null\r\n\tat spring.boot.fainalproject.Service.ReviewService.addReviewForProduct(ReviewService.java:39)\r\n\tat spring.boot.fainalproject.Controller.ReviewController.addReview(ReviewController.java:27)\r\n\tat java.base/
Mohammed Tariq — Today at 9:41 AM
public void addReviewForProduct(Integer orderId, Review review, Integer userId) {
    Customer customer = customerRepository.findCustomerById(userId);
    Order order = orderRepository.findOrderById(orderId);
    Facility facility = facilityRepository.findFacilityById(userId);

    if (order == null) {
        throw new ApiException("Order not found to add review for product");
    }

    if (order.getOrderStatus().equals("Shipped")) {
        if (order.getCustomer_orders() != null && order.getCustomer_orders().getId() == customer.getId()) {
            review.setCustomer(customer);
        }

        if (order.getFacility_orders() != null && order.getFacility_orders().getId() == facility.getId()) {
            review.setFacility(facility);
        }

        reviewRepository.save(review);
    } else {
        throw new ApiException("Your order must be shipped to add a review");
    }
}
Fahadalm13 — Today at 9:48 AM
https://documenter.getpostman.com/view/35088433/2sAXqqdNor
JumlaCycle
JumlaCycle
\[if gte mso 9\]>






\[if gte mso 9\]>

Normal
0




false
false
false

EN-US
X-NONE
AR-SA
























\[if gte mso 9\]>







































...
Image
﻿
# JumlaCycle

## Contact Information

- **Name:** Fahad Almusllam
- **Email:** [F.a.a.m900@gmail.com](mailto:F.a.a.m900@gmail.com)
- **LinkedIn:** [Fahad Almusalam](https://www.linkedin.com/in/fahad-almusalam-a3b094286/)
- **Figma:** [Project Design](https://www.figma.com/design/nNNGhTMIvFlT8xtPiU88oR/JumlaCycle?node-id=0-1&node-type=canvas&t=qiMcDpWnPrpH5chq-0)
- **Postman Documentation:** [Link](<insert-postman-link>)
- **Presentation:** [Canva Presentation](https://www.canva.com/design/DAGQ9ACUzlc/DtIgLE1HbMeTPNDzOfWo_w/edit?utm_content=DAGQ9ACUzlc&utm_campaign=designshare&utm_medium=link2&utm_source=sharebutton)

## Project Overview

**Project Name:** JumlaCycle

The platform is a marketplace designed to connect suppliers with facilities and customers, enabling bulk transactions of products while promoting sustainable practices through recycling. The platform provides a streamlined solution for buying and selling in large quantities, allowing facilities and suppliers to handle bulk orders, manage pricing negotiations, and facilitate the recycling of materials.

## System Flow

1. **Supplier Lists Products:**
   - Suppliers upload product listings for bulk sales.
   - Listings include product details, minimum order quantity, and price per unit.

2. **Facility Makes a Purchase Request:**
   - A facility submits a request for a specific product in bulk, specifying their desired price and quantity.
   - The request is available for suppliers to view and respond.

3. **Supplier Responds with a Price Offer:**
   - Suppliers review facility requests and submit a price offer based on the requested quantity and price.
   - Suppliers can also provide recyclable materials in response to a facility’s recycling request.

4. **Facility Reviews and Approves/Rejects the Offer:**
   - The facility reviews the supplier’s price offer and either approves or rejects it.
   - If approved, the order is processed, and the transaction is completed.
   - If rejected, the facility can wait for new offers from other suppliers.

5. **Supplier Approves or Rejects Requests:**
   - Suppliers can review requests from facilities and either approve or reject them based on their ability to fulfill the order.
   - This gives suppliers control over which requests they can accept based on stock or logistical capabilities.

## Arabic Summary

المنصة عبارة عن سوق مصمم لربط الموردين بالمنشئات والعملاء، مما يتيح إجراء معاملات بالجملة للمنتجات مع تعزيز الممارسات المستدامة من خلال إعادة التدوير. توفر المنصة حلاً مبسطًا للشراء والبيع بكميات كبيرة، مما يسمح للمنشئات والموردين بالتعامل مع الطلبات بالجملة وإدارة مفاوضات التسعير وتسهيل إعادة تدوير المواد.

### تدفق النظام:

1. **المورد يعرض المنتجات:**
   - يقوم الموردون بتحميل قوائم المنتجات للبيع بالجملة.
   - تتضمن القوائم تفاصيل المنتج، وسعر الوحدة.

2. **المنشأة تقدم طلب شراء:**
   - تقدم المنشأة طلباً لمنتج معين بكميات كبيرة، مع تحديد السعر والكمية المطلوبة.
   - يكون الطلب متاحاً للموردين للاطلاع عليه والرد عليه.

3. **المورد يرد بعرض سعر:**
   - يقوم الموردون بمراجعة طلبات المنشآت وتقديم عرض سعر بناءً على الكمية والسعر المطلوبين.
   - يمكن للموردين أيضاً تقديم مواد قابلة لإعادة التدوير استجابةً لطلب إعادة التدوير من المنشأة.

4. **المنشأة تراجع وتوافق/ترفض العرض:**
   - تراجع المنشأة عرض السعر من المورد وتوافق عليه أو ترفضه.
   - إذا تم الموافقة، يتم معالجة الطلب وإتمام المعاملة.
   - إذا تم الرفض، يمكن للمنشأة الانتظار لعروض جديدة من موردين آخرين.

5. **المورد يوافق أو يرفض الطلبات:**
   - يمكن للموردين مراجعة الطلبات من المنشآت ويوافقون أو يرفضونها بناءً على قدرتهم على تلبية الطلب.
   - يمنح ذلك الموردين السيطرة على الطلبات التي يمكنهم قبولها بناءً على المخزون أو القدرات اللوجستية.

## My Work

### Models
- Supplier + Supplier DTO
- Recycle Request
- Price Offer

### Repository
- Supplier
- Recycle Request
- Price Offer 

### Services
- My User Details
- Supplier
- Recycle Request
- Price Offer 

### Controller
- Supplier
- Recycle Request
- Price Offer 

### Controller Advice
- HttpRequestMethodNotSupported
- HttpMessageNotReadable 
- MethodArgument 

### JUnit Tests

#### Repository Tests
- FindCustomerById

#### Service Tests
- addProductSupplierNotFoundTest
- deleteProductNotAccessTest
- getAllOrderTest_NoOrders 
- getAllOrderTest_CustomerOrders 

#### Controller Tests
- TestGetAllProducts
message.txt
6 KB
