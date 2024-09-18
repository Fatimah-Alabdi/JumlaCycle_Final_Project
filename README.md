Name: Fatimah Alabdi

Phone Number: 0560608904

Email: fatimahalabdi22@gmail.com

Linkedin: https://www.linkedin.com/in/fatimah-alabdi-9631a1211/: 

Figma: https://www.figma.com/design/nNNGhTMIvFlT8xtPiU88oR/JumlaCycle?node-id=0-1&node-type=canvas&t=qiMcDpWnPrpH5chq-0

Postman Documentation: https://documenter.getpostman.com/view/35088433/2sAXqqdNor

Presentation: https://www.canva.com/design/DAGQ9ACUzlc/DtIgLE1HbMeTPNDzOfWo_w/edit?utm_content=DAGQ9ACUzlc&utm_campaign=designshare&utm_medium=link2&utm_source=sharebutton


Project Name: JumlaCycle

The platform is a marketplace designed to connect suppliers with facilities and customers, enabling bulk transactions of products while promoting sustainable practices through recycling. The platform provides a streamlined solution for buying and selling in large quantities, allowing facilities and suppliers to handle bulk orders, manage pricing negotiations, and facilitate the recycling of materials.

System Flow:
1.	Supplier Lists Products:
o	Suppliers upload product listings for bulk sales.
o	Listings include product details, minimum order quantity, and price per unit.
2.	Facility Makes a Purchase Request:
o	A facility submits a request for a specific product in bulk, specifying their desired price and quantity.
o	The request is available for suppliers to view and respond.
3.	Supplier Responds with a Price Offer:
o	Suppliers review facility requests and submit a price offer based on the requested quantity and price.
o	Suppliers can also provide recyclable materials in response to a facility’s recycling request.
4.	Facility Reviews and Approves/Rejects the Offer:
o	The facility reviews the supplier’s price offer and either approves or rejects it.
o	If approved, the order is processed, and the transaction is completed.
o	If rejected, the facility can wait for new offers from other suppliers.
5.	Supplier Approves or Rejects Requests:
o	Suppliers can review requests from facilities and either approve or reject them based on their ability to fulfill the order.
o	This gives suppliers control over which requests they can accept based on stock or logistical capabilities.
المنصة عبارة عن سوق مصمم لربط الموردين بالمنشئات والعملاء، مما يتيح إجراء معاملات بالجملة للمنتجات مع تعزيز الممارسات المستدامة من خلال إعادة التدوير. توفر المنصة حلاً مبسطًا للشراء والبيع بكميات كبيرة، مما يسمح للمنشئات والموردين بالتعامل مع الطلبات بالجملة وإدارة مفاوضات التسعير وتسهيل إعادة تدوير المواد.

تدفق النظام:
1.	المورد يعرض المنتجات:
o	يقوم الموردون بتحميل قوائم المنتجات للبيع بالجملة.
o	تتضمن القوائم تفاصيل المنتج، وسعر الوحدة.
2.	المنشأة تقدم طلب شراء:
o	تقدم المنشأة طلباً لمنتج معين بكميات كبيرة، مع تحديد السعر والكمية المطلوبة.
o	يكون الطلب متاحاً للموردين للاطلاع عليه والرد عليه.
3.	المورد يرد بعرض سعر:
o	يقوم الموردون بمراجعة طلبات المنشآت وتقديم عرض سعر بناءً على الكمية والسعر المطلوبين.
o	يمكن للموردين أيضاً تقديم مواد قابلة لإعادة التدوير استجابةً لطلب إعادة التدوير من المنشأة.
4.	المنشأة تراجع وتوافق/ترفض العرض:
o	تراجع المنشأة عرض السعر من المورد وتوافق عليه أو ترفضه.
o	إذا تم الموافقة، يتم معالجة الطلب وإتمام المعاملة.
o	إذا تم الرفض، يمكن للمنشأة الانتظار لعروض جديدة من موردين آخرين.
5.	المورد يوافق أو يرفض الطلبات:
o	يمكن للموردين مراجعة الطلبات من المنشآت ويوافقون أو يرفضونها بناءً على قدرتهم على تلبية الطلب.
o	يمنح ذلك الموردين السيطرة على الطلبات التي يمكنهم قبولها بناءً على المخزون أو القدرات اللوجستية.

My work:
Models :
User
Facility + Facility DTO
Facility Request 
Offer 

Repositiry :
Auth 
Facility 
Facility request 
Offer 

Did All service :
Auth 
Facility 
Facility request 
Offer 
Product 

Controller:
Auth 
Facility 
Facility request 
Offer 
Product 

Controller Advice :
	SQLIntegrity
InvalidData
DataIntegrity 

Junit test :
	
Repository : 
testFindUserById
FindProductBySupplierIdTest 

Service :
deleteProductTest
getProductByIdNotFoundTest
getAllOrderTest_FacilityOrders
Controller : 
registerCustomer
UpdateCustomer









