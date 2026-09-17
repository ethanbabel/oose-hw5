# Task 1

## 1. Model classes

- User
- Professor
- Student
- Course
- Announcement
- Feed

## 2. Client-server interaction

1. The professor signs in, selects a course, writes an announcement in the client (a web browser or mobile application), and clicks Post.
2. The client sends an HTTPS request to the server containing the announcement's content, the course identifier, and the professor's authentication credentials or session token.
3. The server authenticates the request, checks that the professor is authorized to post in that course, and validates the announcement's content. If a check fails, it returns an error for the client to display.
4. The server creates the announcement and saves it in the database with its author, course, and posting time. After the database confirms the write, the server returns a success response, and the professor's client displays the new announcement.
5. When a student opens or refreshes their feed, their client requests the feed from the server. The server authenticates the student, looks up their course enrollments, and queries the database for announcements from those courses. It returns the authorized results, and the client renders them in the student's feed. The clients communicate with the server rather than accessing the database directly.
6. To support live updates, the server can also notify connected clients subscribed to that course when an announcement is saved. Each notified client requests the updated feed and displays the announcement. A student who is offline sees the saved announcement when they next load their feed.

## 3. Design pattern: Observer

**Problem:** A new course announcement affects many students' feeds. The course should not need to know the concrete implementation of every feed or change its posting logic whenever a student joins or leaves.

**Solution:** Treat the course's announcement collection as the subject and the interested students' feeds as observers. Feeds register through a common observer interface. After an announcement is successfully saved, the subject notifies its registered observers, which update themselves or retrieve the new content. Observers can register or unregister as course membership changes. This creates a one-to-many relationship while keeping announcement publishing loosely coupled to feed updates. 
