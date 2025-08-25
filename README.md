# Robust Change Detection, Monitoring, and Alert System on User-Defined AOI Using Multi-Temporal Satellite Imagery

This project aims to build a robust, scalable platform for proactive monitoring and alerting for user-defined Areas of Interest (AOIs), using multi-temporal satellite imagery. The system is designed to filter out irrelevant seasonal or natural fluctuations, providing accurate and reliable change detection.

## Objective

Develop a robust and automated change detection and alert system using multi-temporal imagery. The system will enable cloud/shadow masking and anthropogenic change isolation, empower users with self-defined AOI tools and notification capabilities, and support GIS-compatible output generation for downstream spatial analysis.

## Features

- **Automated Pipeline**: An end-to-end automated pipeline for change detection with robust cloud and shadow masking.
- **Web-Based Platform**: A web-based platform for AOI selection, visualization, and time-series analysis.
- **Alert System**: Email or dashboard alerts for significant anthropogenic changes in user-defined AOIs.
- **GIS-Compatible Outputs**: Generation of GIS-compatible outputs including shapefiles and GeoJSON.

## Backend Architecture

### Framework Options

- **Python (Recommended)**: FastAPI / Flask for APIs
- **Node.js (Alternative)**: Express.js if more comfortable with JavaScript

Choose Python for its powerful image processing and geospatial libraries like Rasterio, NumPy, OpenCV, GDAL, and Scikit-image.

### Backend Flow

1.  **AOI Submission**: Frontend sends polygon coordinates, which are stored in PostgreSQL + PostGIS.
2.  **Satellite Image Fetching**: Fetches images from Bhoonidhi for the specified AOI and date range.
3.  **Preprocessing**: Includes cloud/shadow masking, image resampling, and clipping to the AOI.
4.  **Change Detection**: Compares images from two dates, calculates NDVI, and detects changes based on a predefined threshold.
5.  **Alert System**: Generates alerts if the change area exceeds a certain percentage of the AOI.
6.  **Output Export**: Stores processed outputs as GeoTIFF, Shapefiles, or KML.
7.  **APIs for Frontend**:
    -   `POST /aoi/create`: Submit AOI
    -   `GET /aoi/{id}/status`: Get processing status
    -   `GET /change/{aoi_id}`: Get change percentage and image download link
    -   `GET /alerts/{user_id}`: List of alerts

### Database Tables (PostgreSQL + PostGIS)

-   **users**: `id`, `name`, `email`
-   **aoi**: `id`, `user_id`, `name`, `geometry`
-   **images**: `id`, `aoi_id`, `date`, `image_path`, `cloud_score`
-   **changes**: `id`, `aoi_id`, `date_1`, `date_2`, `change_percent`, `raster_output_path`
-   **alerts**: `id`, `aoi_id`, `date`, `change_level`, `message`

### Tools/Libraries

-   **Web API**: FastAPI / Flask
-   **Geo Processing**: Rasterio, GDAL, NumPy, OpenCV
-   **DB**: PostgreSQL + PostGIS
-   **File Storage**: Local FS / AWS S3
-   **Visualization**: GeoServer (optional)
-   **Automation**: Celery + Redis (optional for background tasks)

## Getting Started

To get started with the project, clone the repository and install the dependencies:

```bash
git clone https://github.com/Dabbe-hub/Geospatial-Change-Detection-and-Alert-System.git
cd your-repo-name
npm install
```

### Development

To run the development server, you will need to run both the frontend and backend servers.

**Backend**

```bash
cd backend
pip install -r requirements.txt
uvicorn main:app --reload
```

The backend server will be available at `http://localhost:8000`.

**Frontend**

```bash
npm install
npm run dev
```

The application will be available at `http://localhost:5173`.

### Building for Production

To build the application for production, use the following command:

```bash
npm run build
```

This will create a `dist` directory with the production-ready files.

## Contributing

Contributions are welcome! Please open an issue or submit a pull request for any changes.
