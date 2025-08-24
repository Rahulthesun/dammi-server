# Dammi Server

A Node.js backend server for uploading images and videos, generating video thumbnails, and storing metadata using Supabase and Cloudflare R2 (S3-compatible storage).

## Features

- **File Upload API**: Accepts image and video uploads via a `/api/upload` endpoint.
- **Authentication**: Verifies users using Supabase JWT tokens.
- **Storage**: Uploads files and video thumbnails to Cloudflare R2 (S3-compatible).
- **Metadata**: Stores and updates file metadata in a Supabase `images` table.
- **Video Thumbnails**: Automatically generates and uploads a thumbnail for each video.
- **CORS Enabled**: Allows cross-origin requests for easy integration with frontends.

## Requirements

- Node.js (v16+ recommended)
- Cloudflare R2 bucket and credentials
- Supabase project with an `images` table
- FFmpeg and FFprobe (static binaries included via npm packages)

## Environment Variables

Create a `.env` file in the project root with the following variables:

```
R2_ENDPOINT=your_r2_endpoint_url
R2_ACCESS_KEY=your_r2_access_key
R2_SECRET_KEY=your_r2_secret_key
R2_BUCKET_NAME=your_r2_bucket_name
NODE_ENV=development
NEXT_PUBLIC_R2_PUBLIC_URL=your_r2_public_url
NEXT_PUBLIC_SUPABASE_URL=your_supabase_url
NEXT_PUBLIC_SUPABASE_ANON_KEY=your_supabase_anon_key
TEMP="/tmp"
```

## Installation

```sh
npm install
```

## Running the Server

```sh
node server.js
```

The server will start on [http://localhost:3001](http://localhost:3001).

## API

### `POST /api/upload`

**Headers:**
- `Authorization: Bearer <supabase_jwt_token>`

**Body:**
- `multipart/form-data` with one or more files under the `files` field.

**Response:**
- `200 OK` with an array of uploaded file info (URLs, thumbnails, etc.)
- Error responses with appropriate status codes and messages.

## File Types Supported

- Images: `jpeg`, `jpg`, `png`, `gif`, `webp`
- Videos: `mp4`, `webm`, `ogg`, `mov` (quicktime)

## Project Structure

- `server.js`: Main server code ([server.js](server.js))
- `.env`: Environment variables
- `package.json`: Dependencies and scripts

## Notes

- Ensure your Supabase project has an `images` table with columns: `id`, `name`, `url`, `thumbnail`, `upload_date`, `user_id`, `size`.
- FFmpeg and FFprobe are required for video thumbnail generation; static binaries are used via npm packages.
- Temporary files are stored in the directory specified by the `TEMP` environment variable.

## License

ISC

---

**Author:**  
[Your