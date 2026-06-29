GET /notifications — it returns list of notifications for the logged in student
GET /notifications/:id — it returns a single notification
PUT /notifications/:id/read — marks a notification as read
GET /notifications/unread/count
{
  "notifications": [
    {
      "id": "uuid",
      "type": "Placement",
      "message": "AffordMed is hiring",
      "isRead": false,
      "timestamp": "2026-06-29T10:00:00"
    }
  ]
}

For real-time I would use WebSockets and when a new notification is created on the backend, the server pushes it directly to the connected student's browser without them needing to refresh