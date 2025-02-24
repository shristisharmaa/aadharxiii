import express from "express";
import mongoose from "mongoose";
import dotenv from "dotenv";
import cors from "cors";
import bodyParser from "body-parser";

dotenv.config();

const app = express();
const PORT = process.env.PORT || 5000;

// Middleware
app.use(
  cors({
    origin: [
      "https://zc-aadhar13-frontend.onrender.com",
      "https://aadhar13.vercel.app",
      "https://aadhar.poornima.org",
    ], // Update with your frontend's hosted URL
    methods: "GET,POST",
    allowedHeaders: "Content-Type",
  })
);
app.use(bodyParser.json());

// MongoDB Connection
mongoose
  .connect(process.env.MONGODB_URI, {
    useNewUrlParser: true,
    useUnifiedTopology: true,
  })
  .then(() => console.log("MongoDB connected"))
  .catch((err) => console.error("MongoDB connection error:", err));

// Schema and Model
const registrationSchema = new mongoose.Schema({
  event: String,
  college: String,
  teamName: String,
  leaderName: String,
  leaderContact: String,
  leaderEmail: String,
  teamSize: String,
  teamMembers: [String],
  transactionId: String,
});

const Registration = mongoose.model("Registration", registrationSchema);

// API Route to Save Data
app.post("/register", async (req, res) => {
  try {
    const registration = new Registration(req.body);
    await registration.save();
    res.status(201).send({ message: "Registration saved successfully" });
  } catch (error) {
    res.status(500).send({ error: "Failed to save registration" });
  }
});

// Start Server
app.listen(PORT, () => console.log(`Server running on port ${PORT}`));
