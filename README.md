# Movie-review-app

#PROJECT DESCRIPTION
The CineCritique project is a full-stack movie review web application designed to provide users with a centralized, easy-to-use platform for discovering movies, submitting genuine reviews, and receiving personalized recommendations. Built on the MERN stack (MongoDB, Express.js, React.js, Node.js), it delivers a responsive, intuitive user interface alongside secure backend services.
Key features include:
	•	User registration and authentication with secure password hashing.
	•	Comprehensive movie database with detailed metadata.
	•	Review and rating system allowing users to submit and view feedback.
	•	Real-time calculation and display of average movie ratings.
	•	Personalized recommendations based on users’ highest-rated genres.
	•	Search and filtering options for efficient movie discovery.
	•	Modular design and RESTful API architecture enabling scalability and maintainability.
The project addresses common challenges in movie discovery, such as fragmented reviews, lack of personalized suggestions, and difficulty accessing authentic user opinions. It emphasizes user engagement through community-driven content while maintaining data security and performance efficiency.
Implementation utilized React components and routing for frontend interactivity; Express.js and MongoDB for backend API and data management; and algorithmic techniques for rating aggregation and recommendation generation. The system was thoroughly tested for reliability, responsiveness, and usability, ensuring a smooth experience across devices.
Overall, CineCritique stands as a robust platform combining entertainment discovery with social interaction, demonstrating practical software engineering skills and modern web development principles.

• POST /api/movies/605c72f7f1d2a913a04f9b88/reviews

code:-
javascript
/ server. js
const express = require(' express');
const mongoose = require ('mongoose');
const app = express ();
app. use (express. json ()) ;
// Connect to MongoDB
mongoose. connect ('mongodb://localhost:27017/cinecritique', {
useNewUrlParser: true,
useUnifiedTopology: true
}) ;
const db = mongoose. connection;
db. on ('error' , console.error bind(console, 'MongoDB connection error: ')) ;
db. once ('open' • () = {
console.log('Connected 'Connected to MongoDB');
1) ;
// Start server
app. listen (3000, () => {
console.1og('Server running on port 3000');
} ) ;
2. Define Schemas & Models
javascript
// models/User•js const mongoose = require ('mongoose');
const userSchema = new mongoose. Schema ( {
username: { type: String, required: true },
email: { type: String, required: true, unique: true },
password: { type: String, required: true }
} ) ;
module. exports = mongoose model ('User', userschema);
javascript
// models/Movie.js const mongoose = require ('mongoose');
const movieSchema = new mongoose. Schema ( {
title: { type: String, required: true },
genre: { type: [String], required: true },
releaseYear: Number, averageRating: { type: Number, default: 0 }
}, { timestamps: true });
module. exports = mongoose model ('Movie', movieschema);
javascript / / models/Review.js const mongoose = require ('mongoose');
const reviewSchema = new mongoose. Schema ( {
userld: { type: mongoose. Schema Types. ObjectId, ref: "'User', required: true },
movield: { type: mongoose. Schema Types ObjectId, ref: 'Movie', required: true },
rating: { type: Number, required: true, min:1, max:5 }r
reviewText: String
}, { timestamps: true });
module. exports = mongoose model('Review', reviewschema);
©
3. User Registration API
javascript / / routes/auth.js const express = require ('express');
const bcrypt = require ('berypt');
const User = require('../models/User');
const router = express. Router ();
router post ('/register', async (reg, res) = {
try { const { username, email, password } = reg.body;
const userExists = await User. findone({ email });
i f (userExists) return res. status (409) json (f message: "Email already registered' });
const hashedPassword = await bcrypt.hash (password, 10);
const user = new User (f username, email, password: hashedPassword }) ;
await user. save () ;
res. status (201) json({ message: 'User registered successfuly' });
} catch (err) {
res. status (500). json(| error: er.message f);
}
} ) ;
module. exports = router;
©
Sample Outputs
Backend Console Output
Connected t o MongoDB
Server running on port 3000
Postman / API Request Examples
• POST /api/auth/register
Request JSON:
json
"username": "john",
"email": "john@example.com" "password": "password123"
}
Response:
json
{
"message": "User registered successfully"
}
• POST /api/movies/605c72f7f1d2a913a04f9b88/reviews
Request JSON:
ison
"userId": "605c72a5f1d2a913a04f9b87", "rating": 5, "reviewText": "Awesome movie!"
巴
Response:
json
"message": "Review submitted successfully",
"review": { "_id": "605c731bf1d2a913a04f9b89", "userId": "605c72a5f1d2a913a04f9b87", "movield": "605c72f7f1d2a913a04f9b88",
"rating": 5, "reviewText": "Awesome movie!"
"createdAt": "2025-11-22T00:00:00.000Z"}}

React Ul Output
• Movie List:
• Inception - Rating: 4.8
• Interstelar - Rating: 4.7
No ratings yet (for movies without reviews)
• Review Form:
• A simple form to add rating (1-5) and text review and submit.


