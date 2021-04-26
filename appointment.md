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
  "success": 1,
  "appointments": [
           {
             "doctor_id" : 47,
             "doctor_first_name" : "Simran",
             "doctor_last_name" : "Kahlon",
             "appointment_date" : "2021-05-01",
             "appointment_start_time" : "10:00",
             "appointment_end_time" : "10:30",
             "appointment_reference_no" : "HGTY65749304"
           },
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
  **Content: Sucessful Response**  
```
{
  "success" : 1,
  "appointment_slots": [
           {
             "slot_date" : "2021-05-01",
             "slot_start_time" : "10:00",
             "slot_end_time" : "10:30",
             "doctor_id" : 47,
             "doctor_first_name" : "Simran",
             "doctor_last_name" : "Kahlon"
           },
           {<appointment_slot>},
           {<appointment_slot>}
         ]
}
```
  **Content: Business Error**
```
{
  "success" : 0,
  "message: "Public Holiday!"
}
```
* **Error Response:** 
  * **Code:** 500  
  **Content:** `{ error : "Something went wrong." }`  
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
    patient_id: int,
    appointment_slot_id: int,
    notes: string
  }
```
* **Success Response:**  
* **Code:** 200  
  **Content: Successful Response**  
```
{
  "success": 1,
  "message" : "Your appointement is booked successfully!",
  "appointment_refernce_no": "GTHYU20210519"
}
```
  **Content: Successful Response**  
```
{
  "success": 0,
  "message" : "Appointment slot is no longer available."
}
```
* **Error Response:**  
  * **Code:** 500  
  **Content:** `{ error : "Something went wrong." }`  
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
    appointment_slot_id: int
  }
```
* **Success Response:**  
* **Code:** 200  
  **Content:**  
```
{
  "success": 1, 
  "message": "Your appointment is cancelled successfully"
}
```
* **Error Response:**  
  * **Code:** 500  
  **Content:** `{ error : "Something went wrong." }`  
  OR  
  * **Code:** 401  
  **Content:** `{ error : error : "You are unauthorized to make this request." }`

A cron will run at midnight to populate the appointment_slots table, considering the doctors
schedule, leaves and public holidays.
