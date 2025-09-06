# Book Recommendation System

## Overview
This project develops a book recommendation system using collaborative filtering, built during my internship at Insider in August 2025. It leverages the Kaggle Book-Crossing dataset to provide personalized book recommendations based on user ratings. The system is implemented with a modular pipeline, a user-friendly Streamlit interface, and deployed on AWS EC2 using Docker for scalability.

## Features
- **Collaborative Filtering**: Uses `NearestNeighbors` with a sparse matrix to recommend books based on user ratings.
- **Interactive UI**: Streamlit-based interface with a dropdown menu for book selection and displays recommended book titles with cover images.
- **Scalable Deployment**: Hosted on AWS EC2 with Docker for efficient and accessible deployment.
- **Modular Codebase**: Organized pipeline with separate stages for data ingestion, validation, transformation, and model training.

## Dataset
The system uses the [Kaggle Book-Crossing dataset](https://www.kaggle.com/datasets/arashnic/book-recommendation-dataset), consisting of:
- `BX-Books.csv`: Book metadata (ISBN, title, author, year, publisher, image URL).
- `BX-Users.csv`: User demographics.
- `BX-Book-Ratings.csv`: User-book ratings.

Filtered to include users with >200 ratings and books with >50 ratings, resulting in 48,321 entries for reliable recommendations.

## Installation
### Prerequisites
- Python 3.7.10
- Conda
- Docker (for deployment)

### Setup
1. Clone the repository:
   ```bash
   git clone https://github.com/BaranParmak/End2End-Book-Recommendation-System.git
   cd End2End-Book-Recommendation-System
   ```
2. Create and activate a Conda environment:
   ```bash
   conda create -n books python=3.7.10 -y
   conda activate books
   ```
3. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```
4. Run the Streamlit app locally:
   ```bash
   streamlit run app.py
   ```

## Project Structure
- `artifacts/`: Stores serialized objects (`model.pkl`, `book_names.pkl`, `final_rating.pkl`, `book_pivot.pkl`).
- `components/`: Pipeline stages for data ingestion, validation, transformation, and model training.
- `config/`: Configuration files (`config.yaml`) for managing data paths and settings.
- `app.py`: Streamlit application for the user interface.
- `template.py`: Script to generate the modular project structure.
- `exception_handler.py` & `log.py`: Custom error handling and logging.

## Usage
1. Launch the Streamlit app:
   ```bash
   streamlit run app.py
   ```
2. Select a book from the dropdown menu.
3. View the top 5 recommended books with their titles and cover images displayed in a 5-column layout.

## Technical Details
- **Data Preprocessing**: Renamed columns for clarity (e.g., `Book-Title` → `title`), filtered data, and merged datasets using `pandas`.
- **Model**: `NearestNeighbors` with `brute` algorithm on a sparse `csr_matrix` of a pivot table (books vs. users).
- **GUI**: Streamlit with a dropdown for book selection and optimized `fetch_poster` function for image loading.
- **Deployment**: Dockerized app deployed on AWS EC2, accessible via port 8501.

## Example
Select "Harry Potter and the Chamber of Secrets" from the dropdown to receive recommendations like other Harry Potter series books or similar titles, displayed with cover images.

## Challenges & Solutions
- **Data Sparsity**: Used `scipy.sparse.csr_matrix` to handle large pivot tables efficiently.
- **Image Loading**: Optimized `fetch_poster` with error handling to improve Streamlit performance.
- **AWS Deployment**: Resolved port configuration issues by adjusting EC2 security groups.

## Future Improvements
- Integrate content-based filtering for hybrid recommendations.
- Test with larger datasets for broader applicability.
- Add user feedback integration for dynamic model updates.

## Deployment on AWS
1. Launch an EC2 instance and install Docker:
   ```bash
   sudo apt-get update -y
   curl -fsSL https://get.docker.com -o get-docker.sh
   sudo sh get-docker.sh
   ```
2. Build and run the Docker image:
   ```bash
   docker build -t baranparmak/bookapp:latest .
   docker run -d -p 8501:8501 baranparmak/bookapp
   ```
3. Push to Docker Hub:
   ```bash
   docker push baranparmak/bookapp:latest
   ```

## Repository
[GitHub Repository](https://github.com/BaranParmak/End2End-Book-Recommendation-System)

## Acknowledgments
- Mentor guidance from Insider’s Optimus team.
- Kaggle for providing the Book-Crossing dataset.
- Streamlit and AWS for enabling user-friendly and scalable deployment.
