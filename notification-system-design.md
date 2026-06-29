Stage 1:

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


Stage 2:


CREATE TABLE notifications (
  id uuid PRIMARY KEY,
  student_id INT NOT NULL,
  type VARCHAR(20) CHECK (type IN ('Event', 'Result', 'Placement')),
  message TEXT,
  is_read BOOLEAN DEFAULT false,
  created_at TIMESTAMP DEFAULT NOW()
);

As data grows to millions of rows, the main problems will be slow queries and disk space so to fix that I would add indexes on student_id and created_at, use pagination in the API so we never fetch all records at once, and also archive old notifications to a separate table after 6 months