# 🌍✨ Robust Change Detection, Monitoring & Alert System on User-Defined AOI Using Multi-Temporal Satellite Imagery

> **A scalable platform for proactive monitoring & alerting of user-defined Areas of Interest (AOIs) using multi-temporal satellite imagery.**
> Filters out irrelevant seasonal/natural fluctuations for accurate & reliable change detection.

---

## 🎯 Objective

Develop a **robust, automated change-detection & alert system** using multi-temporal imagery.
Key goals:

* 🛰️ Cloud & shadow masking + anthropogenic change isolation
* 🗺️ Empower users with self-defined AOI tools & notifications
* 🧭 Support **GIS-compatible outputs** for downstream spatial analysis

---

## ✨ Features

* 🚀 **Automated Pipeline** – End-to-end change detection with cloud/shadow masking
* 🌐 **Web Platform** – AOI selection, visualization & time-series analysis
* 📢 **Alert System** – Email/dashboard alerts for significant anthropogenic changes
* 🗂️ **GIS Outputs** – Shapefiles, GeoJSON, and other GIS-compatible formats

---

## 🏗️ Backend Architecture

### 🧰 Framework Options

* 🐍 **Python (Recommended)**: FastAPI / Flask for APIs
* 💻 **Node.js (Alternative)**: Express.js if you prefer JavaScript

> Choose **Python** for its powerful geospatial libraries: `Rasterio`, `NumPy`, `OpenCV`, `GDAL`, `Scikit-image`.

---

### 🔄 Backend Flow

1. 📌 **AOI Submission** – Frontend sends polygon coords → stored in **PostgreSQL + PostGIS**
2. 🛰️ **Satellite Image Fetching** – Pulls imagery from *Bhoonidhi* for AOI & date range
3. ⚙️ **Preprocessing** – Cloud/shadow masking, resampling, AOI clipping
4. 🔍 **Change Detection** – NDVI calculation + change thresholding
5. 🚨 **Alert System** – Alerts if change area > % threshold of AOI
6. 💾 **Output Export** – GeoTIFF, Shapefile, or KML outputs
7. 🔗 **APIs for Frontend**:

   * `POST /aoi/create` → Submit AOI
   * `GET /aoi/{id}/status` → Check processing status
   * `GET /change/{aoi_id}` → Change % & download link
   * `GET /alerts/{user_id}` → List alerts

---

### 🗄️ Database Schema (PostgreSQL + PostGIS)

| Table       | Columns                                                                    |
| ----------- | -------------------------------------------------------------------------- |
| **users**   | `id`, `name`, `email`                                                      |
| **aoi**     | `id`, `user_id`, `name`, `geometry`                                        |
| **images**  | `id`, `aoi_id`, `date`, `image_path`, `cloud_score`                        |
| **changes** | `id`, `aoi_id`, `date_1`, `date_2`, `change_percent`, `raster_output_path` |
| **alerts**  | `id`, `aoi_id`, `date`, `change_level`, `message`                          |

---

### 🛠️ Tools & Libraries

* **Web API**: FastAPI / Flask
* **Geo Processing**: Rasterio, GDAL, NumPy, OpenCV
* **Database**: PostgreSQL + PostGIS
* **Storage**: Local FS / AWS S3
* **Visualization**: GeoServer *(optional)*
* **Automation**: Celery + Redis *(optional)*

---

## 🚀 Getting Started

Clone the repository & install dependencies:

```bash
git clone https://github.com/Dabbe-hub/Geospatial-Change-Detection-and-Alert-System.git
cd your-repo-name
npm install
```

---

### 🛠️ Development

Run **backend**:

```bash
cd backend
pip install -r requirements.txt
uvicorn main:app --reload
```

> Backend runs at [http://localhost:8000](http://localhost:8000)

Run **frontend**:

```bash
npm install
npm run dev
```

> App available at [http://localhost:5173](http://localhost:5173)

---

### 📦 Build for Production

```bash
npm run build
```

> Generates a `dist` folder with production files.

---

## 🤝 Contributing

💡 **Contributions are welcome!**
Open an issue or submit a pull request to enhance features, fix bugs, or improve docs.

---

### 🌟 Enjoy building with cutting-edge geospatial change detection!
