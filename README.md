# GenViva: AI Powered Presentation Coach

## Overview

Presentations are an important skill in academics and professional environments. They test not only technical knowledge but also communication, confidence, clarity, and the ability to handle questions.

However, improving presentation skills is often difficult. Most people depend on friends, peers, or mentors for practice, but feedback can be subjective, inconsistent, and may not identify specific problems such as filler words, nervousness, poor pacing, weak explanations, or difficulty answering technical questions.

**GenViva** is a Generative AI powered presentation coach designed to help users practice and improve independently. It acts as an AI evaluator that analyzes a presentation from multiple perspectives:

- How well the content is explained
- How confidently the speaker delivers it
- Speech patterns and fluency
- Facial expressions and confidence indicators
- Ability to answer project-specific viva questions

The system provides a confidence score, identifies weak areas, generates personalized viva questions, evaluates answers, and creates an improvement loop where users can compare multiple attempts and track progress.

---

# Key Features

## 🎤 Multi-Modal Presentation Analysis

Unlike traditional tools that focus on only one aspect of presentation delivery, GenViva combines multiple inputs:

- Presentation slides (`.pptx` / `.pdf`)
- Presentation recording (video + audio)

The system evaluates both **what the user presents** and **how they present it**.

---

# 📝 Presentation Content Analysis

GenViva extracts text from uploaded presentation files using:

- `python-pptx` for PowerPoint files
- `PyMuPDF` for PDF files

The extracted slide content is used for:

- Understanding the project context
- Measuring how well the speaker explains slide information
- Generating relevant viva questions

The system calculates a **Content Coverage Score** by comparing important keywords from the slides with the speaker's transcript.

This helps identify whether the speaker is explaining the actual content instead of only reading or giving a shallow overview.

---

# 🎙️ Speech Analysis

The uploaded video is processed to extract audio using FFmpeg.

The audio is converted into a suitable format:

- 16 kHz sampling rate
- Mono channel WAV file

The system uses **OpenAI Whisper** for speech transcription and extracts timestamped speech segments.

The following speech features are analyzed:

### Speaking Pace

Measures words per minute to determine whether the speaker is speaking too slowly or too quickly.

### Filler Word Detection

Tracks unnecessary filler words such as:

- um
- uh
- like
- basically
- actually
- you know

### Pause Detection

Identifies long pauses that may indicate hesitation or lack of confidence.

### Voice Confidence

Using audio energy analysis with Librosa, the system estimates vocal confidence based on consistency and strength of speech.

These features are combined to calculate a **Fluency Score** and **Vocal Confidence Score**.

---

# 🙂 Facial Expression and Confidence Analysis

GenViva analyzes the presentation video using:

- OpenCV
- DeepFace

Frames are sampled from the video at regular intervals to analyze facial expressions.

The system tracks:

- Neutral expressions
- Positive expressions
- Fear indicators
- Sadness indicators
- Face visibility

This helps estimate how confident and comfortable the speaker appears during the presentation.

The output is a **Facial Confidence Score**.

---

# 📊 Multi-Modal Confidence Score

The individual analysis modules are combined into a single confidence score.

The score considers:

| Component | Weight |
|---|---:|
| Facial Confidence | 35% |
| Vocal Confidence | 30% |
| Fluency | 20% |
| Content Delivery | 15% |

This provides a measurable evaluation of presentation performance instead of subjective feedback.

---

# 🤖 AI Powered Viva Simulation

A major feature of GenViva is its ability to simulate a project viva.

Instead of asking generic questions, the system generates questions based on:

- Uploaded slides
- Presentation transcript
- Identified weak areas

The system uses a Retrieval Augmented Generation (RAG) pipeline:

1. Slide content and transcript are converted into text chunks.
2. Sentence Transformer embeddings are generated.
3. Embeddings are stored using FAISS vector search.
4. Relevant project information is retrieved.
5. Google Gemini generates personalized viva questions.

The generated questions focus on:

- Project understanding
- Technical depth
- Missing explanations
- Weak areas detected during analysis

This creates a viva experience closer to an actual project evaluation.

---

# 💡 Viva Answer Evaluation

After answering generated questions, the user's responses are evaluated using Generative AI.

Each answer is scored based on:

### Relevance
How accurately the answer addresses the question.

### Technical Depth
How well the user explains concepts and implementation details.

### Clarity
How structured and understandable the explanation is.

The final answer quality score helps measure viva readiness.

---

# 🔄 Feedback Improvement Loop

GenViva follows an iterative improvement approach.

### First Attempt

The user uploads:

- Presentation slides
- Presentation video

The system generates:

- Confidence score
- Speech analysis
- Facial analysis
- Weak areas
- Viva questions


### Feedback Stage

The user receives:

- Strengths
- Areas for improvement
- Detailed viva feedback


### Second Attempt

The user uploads an improved presentation.

The system runs the analysis again and compares:

- Initial confidence score
- Improved confidence score
- Viva performance

This allows users to measure actual improvement over multiple practice sessions.

---






---

# Technology Stack

## Frontend

- Streamlit

## AI Models

- Google Gemini 2.5 Flash
- OpenAI Whisper
- Sentence Transformers
- DeepFace

## Natural Language Processing

- Retrieval Augmented Generation (RAG)
- FAISS Vector Search
- Text Embeddings

## Audio Processing

- FFmpeg
- Librosa

## Computer Vision

- OpenCV

## Document Processing

- python-pptx
- PyMuPDF

## Programming Language

- Python

---

# Implementation Highlights

- Automatic presentation text extraction from PPT and PDF files
- AI-based speech transcription
- Multi-feature speech analysis pipeline
- Facial emotion and confidence estimation
- Retrieval-based personalized viva generation
- AI evaluation of viva answers
- Automated weak area detection
- Multi-attempt progress tracking

---

# Future Improvements

## Real-Time Presentation Feedback

Currently, GenViva evaluates recorded presentations. Future versions can provide:

- Live confidence monitoring
- Real-time speaking suggestions
- Instant viva interaction


## Advanced Body Language Analysis

Additional features can include:

- Eye gaze tracking
- Gesture recognition
- Posture analysis


## Personalized Learning Plans

By tracking multiple attempts, GenViva can generate:

- Long-term improvement reports
- Personalized practice plans
- Repeated weakness identification


---

# Conclusion

GenViva combines Generative AI, speech processing, computer vision, and retrieval-based question generation to create an intelligent presentation improvement assistant.

Instead of only evaluating a presentation, GenViva helps users understand their weaknesses, practice effectively, prepare for technical discussions, and continuously improve through feedback.

It transforms presentation preparation from a subjective practice process into a measurable AI-guided learning experience.
