**GET /getAppointments/:id**
----
  Returns all the active appointments for a patient.
* **URL Params**  
  *Required:* `id=[integer]`
* **Data Params**  
  None
* **Headers**  
  Content-Type: application/json  
  Authorization: Bearer `<OAuth Token>`
* **Success Response:**  
* **Code:** 200  
  **Content:**  
```
{
  appointments: [
           {<appointment_object>},
           {<appointment_object>},
           {<appointment_object>}
         ]
}
```
* **Error Response:** 
  * **Code:** 500  
  **Content:** `{ error : "Something went wrong." }`  
  OR
  * **Code:** 404  
  **Content:** `{ error : "Patient doesn't exist" }`  
  OR  
  * **Code:** 401  
  **Content:** `{ error : error : "You are unauthorized to make this request." }`

**GET /bookAppointment/:date**
----
  Returns all the active slots for that date.
* **URL Params**  
  *Required:* `date=[string]`
* **Data Params**  
  None
* **Headers**  
  Content-Type: application/json  
  Authorization: Bearer `<OAuth Token>`
* **Success Response:**  
* **Code:** 200  
  **Content:**  
```
{
  appointment_slots: [
           {<appointment_slot>},
           {<appointment_slot>},
           {<appointment_slot>}
         ]
}
```
* **Error Response:** 
  * **Code:** 500  
  **Content:** `{ error : "Something went wrong." }`  
  OR
  * **Code:** 404  
  **Content:** `{ error : "Public Holiday" }`  
  OR  
  * **Code:** 401  
  **Content:** `{ error : error : "You are unauthorized to make this request." }`

**POST /bookAppointment**
----
  Book appointment for patient
* **URL Params**  
  None
* **Headers**  
  Content-Type: application/json  
* **Data Params**  
```
  {
    patient_id: string,
    appointment_slot_id: string,
    notes: string
  }
```
* **Success Response:**  
* **Code:** 200  
  **Content:**  
```
{
  message : "Your appointement is booked successfully!",
  appointment_refernce_no: "GTHYU20210519"
}
```
* **Error Response:**  
  * **Code:** 500  
  **Content:** `{ error : "Something went wrong." }`  
  OR
   * **Code:** 404  
  **Content:** `{ error : "Appointment slot is no longer available." }`  
  OR  
  * **Code:** 401  
  **Content:** `{ error : error : "You are unauthorized to make this request." }`

**POST /cancelAppointment**
----
  Cancel appointment for patient
* **URL Params**  
  None
* **Headers**  
  Content-Type: application/json  
* **Data Params**  
```
  {
    appointment_slot_id: string,
    reason: string
  }
```
* **Success Response:**  
* **Code:** 200  
  **Content:**  
```
{
  success: "Your appointment is cancelled successfully"
}
```
* **Error Response:**  
  * **Code:** 500  
  **Content:** `{ error : "Something went wrong." }`  
  OR  
  * **Code:** 401  
  **Content:** `{ error : error : "You are unauthorized to make this request." }`
