// Web Video Downloader
// Single-file project overview + code snippets for a minimal, safe web video downloader
// Usage: follow README at bottom. This file contains frontend (React) and backend (Node/Express) code.

---

// frontend: src/App.jsx
import React, { useState } from 'react'

export default function App() {
  const [url, setUrl] = useState('')
  const [loading, setLoading] = useState(false)
  const [error, setError] = useState(null)

  async function handleDownload(e) {
    e.preventDefault()
    setError(null)
    if (!url) return setError('Masukkan URL file video publik (contoh: .mp4 direct link)')
    setLoading(true)
    try {
      const resp = await fetch(`/api/download?url=${encodeURIComponent(url)}`)
      if (!resp.ok) throw new Error(await resp.text())
      const blob = await resp.blob()
      const contentDisposition = resp.headers.get('content-disposition')
      let filename = 'video'
      if (contentDisposition) {
        const m = /filename="?([^\"]+)"?/.exec(contentDisposition)
        if (m) filename = m[1]
      }
      const urlBlob = URL.createObjectURL(blob)
      const a = document.createElement('a')
      a.href = urlBlob
      a.download = filename
      document.body.appendChild(a)
      a.click()
      a.remove()
      URL.revokeObjectURL(urlBlob)
    } catch (err) {
      setError(err.message)
    } finally {
      setLoading(false)
    }
  }

  return (
    <div className="min-h-screen flex items-center justify-center p-6">
      <div className="max-w-xl w-full bg-white shadow-lg rounded-2xl p-6">
        <h1 className="text-2xl font-semibold mb-3">Web Video Downloader (Minimal)</h1>
        <form onSubmit={handleDownload}>
          <label className="block text-sm font-medium mb-1">Direct video URL</label>
          <input
            value={url}
            onChange={e => setUrl(e.target.value)}
            placeholder="https://example.com/video.mp4"
            className="w-full border rounded p-2 mb-3"
          />
          <div className="flex items-center gap-3">
            <button className="px-4 py-2 rounded bg-blue-600 text-white" disabled={loading}>
              {loading ? 'Downloading...' : 'Download'}
            </button>
            <button type="button" className="px-3 py-2 rounded border" onClick={() => { setUrl('') ; setError(null) }}>
              Reset
            </button>
          </div>
          {error && <p className="mt-3 text-red-600">{error}</p>}
        </form>

        <hr className="my-4" />
        <p className="text-sm text-gray-600">Catatan: Aplikasi ini hanya untuk mengunduh file video publik (direct file URL). Tidak mendukung situs yang memerlukan login, API resmi, atau protected streaming (DRM). Gunakan secara bertanggung jawab dan jangan melanggar hak cipta.</p>
      </div>
    </div>
  )
}

---

// backend: server.js (Node + Express)
// Purpose: simple proxy that streams a remote video file to the client with safety checks.

/*
Install dependencies:
  npm init -y
  npm i express node-fetch@2 helmet express-rate-limit
Run:
  node server.js

This server exposes GET /api/download?url=ENCODED_URL
It validates the URL, enforces size limit, and streams the response.
*/

const express = require('express')
const fetch = require('node-fetch')
const helmet = require('helmet')
const rateLimit = require('express-rate-limit')
const { pipeline } = require('stream')
const { URL } = require('url')

const app = express()
app.use(helmet())
app.use(express.json())

// Basic rate limiting
app.use(rateLimit({ windowMs: 60 * 1000, max: 30 }))

// Allow serving frontend build from ./public (optional)
app.use(express.static('public'))

function isHttpUrl(s) {
  try { new URL(s); return true } catch (e) { return false }
}

app.get('/api/download', async (req, res) => {
  const remote = req.query.url
  if (!remote) return res.status(400).send('Missing url parameter')
  if (!isHttpUrl(remote)) return res.status(400).send('Invalid url')

  // Only allow http/https
  const parsed = new URL(remote)
  if (!['http:', 'https:'].includes(parsed.protocol)) return res.status(400).send('Protocol not allowed')

  // Only allow likely video extensions for safety (basic check)
  const allowedExt = ['.mp4', '.webm', '.mkv', '.mov', '.flv']
  if (!allowedExt.some(e => parsed.pathname.toLowerCase().endsWith(e))) {
    // not strictly required, but safer to prevent misuse
    return res.status(400).send('URL does not point to a supported video file (must end with .mp4/.webm/.mov/.mkv/.flv)')
  }

  try {
    // Make a HEAD request first to check content-type and length
    const head = await fetch(remote, { method: 'HEAD' })
    if (!head.ok) return res.status(502).send('Upstream HEAD request failed')
    const cType = head.headers.get('content-type') || ''
    if (!cType.startsWith('video/')) {
      return res.status(400).send('Remote resource is not a video')
    }
    const contentLength = head.headers.get('content-length')
    const MAX_BYTES = 200 * 1024 * 1024 // 200 MB limit
    if (contentLength && Number(contentLength) > MAX_BYTES) {
      return res.status(413).send('Remote file too large')
    }

    // Now stream the GET response
    const upstream = await fetch(remote)
    if (!upstream.ok) return res.status(502).send('Upstream GET request failed')

    res.setHeader('Content-Type', upstream.headers.get('content-type') || 'application/octet-stream')
    // suggest filename
    const filename = parsed.pathname.split('/').pop() || 'video'
    res.setHeader('Content-Disposition', `attachment; filename="${filename}"`)

    // Stream pipeline
    pipeline(upstream.body, res, (err) => {
      if (err) console.error('Stream error:', err)
    })
  } catch (err) {
    console.error(err)
    res.status(500).send('Server error')
  }
})

const PORT = process.env.PORT || 4000
app.listen(PORT, () => console.log(`Server listening on ${PORT}`))

---

// README (run instructions)

/*
1) Struktur proyek minimal:

  /project-root
    /public            (optional: build of frontend goes here)
    server.js          (backend)
    package.json
    /frontend
      src/App.jsx      (frontend React component)

2) Menjalankan backend (development):
   - Buat package.json (npm init -y)
   - npm i express node-fetch@2 helmet express-rate-limit
   - node server.js
   - Buka http://localhost:4000 (frontend static files if disimpan di /public) atau jalankan frontend dev separately.

3) Menjalankan frontend (create-react-app / Vite):
   - Buat proyek React (CRA or Vite), ganti src/App.jsx dengan kode di atas.
   - Saat development, gunakan proxy di package.json React: "proxy": "http://localhost:4000"
   - npm start untuk frontend dev server.

4) Catatan penting dan batasan hukum:
   - Aplikasi ini hanya untuk URL file video publik (direct links). Jangan gunakan untuk mengunduh materi berhak cipta tanpa izin.
   - Mengunduh dari layanan seperti YouTube, Netflix, Disney+, dll. sering melanggar Terms of Service dan/atau hukum hak cipta. Aplikasi ini tidak mendukung bypass proteksi (DRM) atau scraping terlarang.
   - Jika kamu ingin fitur untuk layanan tertentu, gunakan API resmi (jika tersedia) atau minta izin pemilik konten.

5) Fitur yang bisa ditambahkan:
   - Autentikasi dan logging untuk audit
   - Queue + worker untuk file besar
   - Range-request support (untuk resume)
   - Convert atau compress server-side (ffmpeg)
*/
