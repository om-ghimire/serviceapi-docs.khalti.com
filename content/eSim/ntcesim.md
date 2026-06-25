# NTC E-SIM

This document describes the NTC e-SIM purchase API. Use this endpoint to sell NTC e-SIMs to end customers

---

### 1. Purchase (NTC e-SIM)

This endpoint processes e-SIM purchase requests and returns activation information on success.

**POST**  
`{{base_url}}/api/use/ntc-e-sim/`

#### Request Body (JSON)

<pre><code class="json">
{
    "token": "<your token>",
    "reference": "unique-reference-123",
    "amount": 90,
    "name": "Test Bahadur Kansakar",
    "dob": "2000-01-01",
    "address": "Panipokhari",
    "email": "ram.bahadur@gmail.com",
    "father": "Hari Bahadur Shrestha",
    "grandfather": "Man Bahadur Shrestha",
    "mother": "Sita Devi Shrestha",
    "document_number": "12345678",
    "issue": "2088-05-15",
    "pp_photo1": "+fpfHqY9vUSABjI8vr+...",
    "pp_photo2": "+fpfHqY9vUSABjI8vr+...",
    "pp_photo3": "+fpfHqY9vUSABjI8vr+...",
    "t_n_c": true
}
</code></pre>

**Field notes**

- **amount:** Fixed at `90` (NPR) for the NTC e-SIM product. Do not change.
- **reference:** Unique string per request; duplicate references will be rejected.
- **issue:** Issue date in ISO Gregorian format `YYYY-MM-DD`.
- **pp_photo1/2/3:** Base64-encoded image strings (JPEG/PNG). Maximum 2 MB per image.
- **t_n_c:** Boolean; must be `true` to indicate customer accepted terms and conditions.

---

#### Success Response

<pre><code class="json">
{
    "status": true,
    "state": "Success",
    "detail": "Transaction Completed.",
    "message": "Transaction Completed",
    "credits_consumed": 90.0,
    "credits_available": 99985279214.4199,
    "extra_data": {
        "name": "Shrestha Shrestha",
        "dob": "2000-01-01",
        "address": "Panipokhari",
        "email": "ram.bahadur@gmail.com",
        "father": "Hari Bahadur Shrestha",
        "grandfather": "Man Bahadur Shrestha",
        "mother": "Sita Devi Shrestha",
        "document_number": "12345678",
        "issue": "2088-05-15",
        "pp_photo1": "https://test.com/ntc/esim/2026-06-25/7e038ade8d63405bb7x1933e87adb1f2d/pp_photo1_20260625093944.png?AWSAccessKeyId=AKxIAS7HNYSJPMICKDGHW&Signature=IAhN54WmHVjMP%2FZ7yPK3P4mhQI8%3D&Expires=178238cxx0744",
        "pp_photo2": "https://test.com/ntc/esim/2026-06-25/cb8122b253f0432b917998b069d86610/pp_photo2_20260625093944.png?AWSAccessKeyId=AKIAS7HNYSJPMICKDGHW&Signature=XhX1d5zUc6aVQaVelKkZj7jeUIU%3D&Expires=1782380745",
        "pp_photo3": "https://test.com/ntc/esim/2026-06-25/f0b49f79773744b1938248734c01e5f8/pp_photo3_20260625093945.png?AWSAccessKeyId=AKIAS7HNYSJPMICKDGHW&Signature=YkpJgPrDABSixS0Uzr9ziSNl7tI%3D&Expires=1782380745",
        "t_n_c": true
    },
    "id": 237292
}
</code></pre>

---

#### Error Responses

Validation error (invalid parameters):

<pre><code class="json">
{
    "status": false,
    "error_code": "1010",
    "message": "Validation error",
    "error": "invalid_parameters",
    "details": {
        "amount": "enter valid amount"
    },
    "state": "Error"
}
</code></pre>

Duplicate reference id:

<pre><code class="json">
{
    "status": false,
    "error_code": "1013",
    "message": "Request with duplicate reference id obtained",
    "error": "duplicate_request",
    "state": "Error"
}
</code></pre>

**Note:** Upon successful registration we will send a confirmation email to the user containing the SIM details.

