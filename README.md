<div hidden>
```
@startuml

' Enum for Status
enum OrderStatus {
Pending
Processed
Delivered
}

enum DeliveryStatus {
Scheduled
InTransit
Completed
}

enum RouteStatus {
Optimizing
Completed
Failed
}

enum VehicleStatus {
Available
InUse
Maintenance
Unavailable
}

' BaseEntity, extended by every other class
class BaseEntity {
+id: int
+createdAt: Date
+updatedAt: Date
}

' User entity
class User {
+username: string
+password: string
+email: string
+role: string
}

' Product entity
class Product {
+price: double
+weight: double
+name: string
+description: string
+stockQuantity: int
+imageUrl: string
}

' Address Value Object
class Address {
+country: string
+city: string
+zipcode: string
+street: string
}

' Location Value Object (for geographical coordinates)
class Location {
+latitude: double
+longitude: double
+address: Address
+name: string
}

' Order entity
class Order {
+totalAmount: double
+deliveryDate: Date
+deliveryAddress: Address
+phoneNumber: string
+items: List<Product>
+status: OrderStatus
+note: string
}

' Route entity
class Route {
+totalDuration: int
+totalDistance: double
+optimized: bool
+startTime: Date
+endTime: Date
+waypoints: List<Location>
+status: RouteStatus
}

' Delivery entity
class Delivery {
+status: DeliveryStatus
+routeId: int
+vehicleId: int
+orderList: List<Order>
+deliveryTimeWindow: TimeWindow
+trackingId: string
}

' Vehicle entity
class Vehicle {
+licensePlate: string
+capacity: double
+status: VehicleStatus
}

class OrderItem {
+product: Product
+quantity: int
}

skinparam class {
BackgroundColor White
ArrowColor Black
BorderColor Black
}


' Relations between entities
BaseEntity <|-- User
BaseEntity <|-- Product
BaseEntity <|-- Order
BaseEntity <|-- Delivery
BaseEntity <|-- Route
BaseEntity <|-- Vehicle

Order "1" *-- "*" Product : contains
Delivery "1" *-- "*" Order : delivers
Route "1" *-- "*" Location : contains
Vehicle "1" *-- "1" Delivery : delivers
Order "1" *-- "1" Address : has
Delivery "1" *-- "1" Route : associated with
Location "1" *-- "1" Address : has
Order "1" *-- "*" OrderItem : contains
@enduml

```
</div>

![](firstDiagram.svg)
