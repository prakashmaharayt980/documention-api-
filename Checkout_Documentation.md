# Checkout API Documentation

This document outlines the API details for the checkout process in Fatafat Sewa.

## 1. Create Order

**Endpoint:** `POST /v1/orders`

**Description:** Creates a new order with the selected products, shipping address, and payment method.

### Request Payload

The request body should be a JSON object with the following fields:

| Field | Type | Required | Description |
| :--- | :--- | :--- | :--- |
| `phone` | `string` | Yes | User's phone number. |
| `full_name` | `string` | Yes | User's full name. |
| `products` | `array` | Yes | List of products to order. |
| `products[].product_id` | `number` | Yes | ID of the product. |
| `products[].quantity` | `number` | Yes | Quantity of the product. |
| `shipping_address_id` | `number` | Yes | ID of the selected shipping address. |
| `total_amount` | `number` | Yes | Final total amount including shipping and discounts. |
| `payment_type` | `string` | Yes | Payment method (e.g., `esewa`, `khalti`, `cod`). Formatted as snake_case. |
| `promo_code` | `string` | No | Applied promo code, if any. |
| `delivery_partner` | `string` | Yes | Name of the selected delivery partner. |
| `delivery_partner_user_id` | `string` | No | User ID for the delivery partner service, if applicable. |
| `recipient_type` | `string` | Yes | `myself` or `other`. |
| `gift_recipient_name` | `string` | No | Name of the recipient if `recipient_type` is `other`. |
| `gift_recipient_phone` | `string` | No | Phone of the recipient if `recipient_type` is `other`. |
| `gift_message` | `string` | No | Optional gift message. |
| `shipping_cost` | `number` | Yes | Calculated shipping cost (currently 0). |

#### Example Request

```json
{
  "phone": "9800000000",
  "full_name": "John Doe",
  "products": [
    {
      "product_id": 101,
      "quantity": 2
    },
    {
      "product_id": 202,
      "quantity": 1
    }
  ],
  "shipping_address_id": 15,
  "total_amount": 2500,
  "payment_type": "esewa",
  "promo_code": "SAVE10",
  "delivery_partner": "Fatafat Sewa",
  "delivery_partner_user_id": null,
  "recipient_type": "myself",
  "gift_recipient_name": null,
  "gift_recipient_phone": null,
  "gift_message": null,
  "shipping_cost": 0
}
```

### Response

**Success Response (200 OK / 201 Created)**

Returns the created order details. The client expects an `id` field to proceed with payment.

```json
{
  "id": "ord_123456789",
  "status": "pending",
  "total_amount": 2500,
  "message": "Order created successfully"
  // ... other order details
}
```

**Note:** The client checks for `res.id` or `res.data.id` to initiate the payment flow.

### Error Response

**400 Bad Request**

*   Validation errors (missing fields, invalid product IDs).
*   Out of stock items.

## 2. Payment Flow

After a successful order creation, the client initiates the payment process based on `payment_type`.

*   **eSewa:** Redirects to eSewa payment gateway with the Order ID (`pid`) and amount.
*   **Khalti:** Initiates Khalti payment (currently mock/test mode).
*   **COD:** Redirects directly to the Success Page.

**Success URL:** `/checkout/Successpage?oid={order_id}`
**Failure URL:** `/checkout/failed`

## 3. Shipping Address API

Manage user shipping addresses.

| Method | Endpoint | Description |
| :--- | :--- | :--- |
| `GET` | `/v1/user/shipping-addresses` | List all shipping addresses. |
| `POST` | `/v1/user/shipping-addresses` | Create a new shipping address. |
| `PUT` | `/v1/user/shipping-addresses/{id}` | Update a specific address. |
| `DELETE` | `/v1/user/shipping-addresses/{id}` | Delete a specific address. |

## 4. Recipient Details Logic

The `recipient_type` field controls whose information is used for delivery:

*   **`recipient_type: "myself"`**:
    *   The system uses the **User's** registered name and phone number.
    *   `gift_recipient_name` and `gift_recipient_phone` are ignored.

*   **`recipient_type: "other"`**:
    *   The system uses the provided **Gift Recipient's** details.
    *   **Required Fields**: `gift_recipient_name`, `gift_recipient_phone`.
    *   **Optional**: `gift_message`.
