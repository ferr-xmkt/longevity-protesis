# Despliegue — Landing Prótesis Longevity ForCell

## Contexto
- Landing estática (HTML + CSS inline + 8 imágenes en `img/`).
- Destino propuesto: subdirectorio estático en `longevityforcell.cl/protesis/` (no se toca WordPress, solo se sube la carpeta por FTP/cPanel).
- Las imágenes actuales en `img/` son placeholders — reemplazar por fotos reales antes de subir.

## Estado del sitio
Al momento de empacar (22 abril 2026), `longevityforcell.cl` no respondía. Verificar que esté operativo antes de desplegar.

## Pasos en la otra PC

### 1. Recibir el bundle
Copia `landing-protesis.bundle` a una carpeta de trabajo (ej. `~/Documents/`).

### 2. Clonar desde el bundle
```bash
cd ~/Documents
git clone landing-protesis.bundle landing-protesis
cd landing-protesis
```

### 3. Reemplazar imágenes placeholder por fotos reales
Archivos a reemplazar en `img/`:
- `hero-clinic.jpg` — foto principal (Clínica Monteblanco)
- `dr-mardones.jpg` — Dr. Rodrigo Mardones
- `dr-ilic.jpg` — Dr. Tomás Ilić
- `pabellon.jpg` — pabellón quirúrgico
- `surgery.jpg` — cirugía en curso
- `recovery.jpg` — paciente en recuperación
- `patient-walking.jpg` — paciente caminando post-op
- `doctor.jpg` — médico (usar donde se requiera foto neutral)

Mantén los mismos nombres y extensiones. Optimiza a <200KB cada una (usa squoosh.app o `cwebp`).

### 4. Commit de las fotos reales
```bash
git add img/
git commit -m "Reemplaza placeholders por fotos reales"
```

### 5. Crear repo en GitHub (desde esa PC donde tienes credenciales)
```bash
gh repo create longevity-forcell-landing --private --source=. --remote=origin --push
```
(o desde github.com manualmente → agregar remote → push)

### 6. Desplegar en WordPress hosting (subdirectorio)

**Opción A — FTP/SFTP**:
1. Conectar al hosting (credenciales en tu manager).
2. Ir a la raíz pública (usualmente `/public_html/` o `/www/`).
3. Crear carpeta `protesis/`.
4. Subir `index.html` + carpeta `img/` dentro de `protesis/`.
5. Verificar: `https://longevityforcell.cl/protesis/`

**Opción B — cPanel File Manager**:
1. Login cPanel → File Manager.
2. Navegar a `public_html/`.
3. Crear carpeta `protesis`.
4. Upload → seleccionar `index.html` y carpeta `img/` (o un zip y extract).

### 7. Verificación post-despliegue
- [ ] `https://longevityforcell.cl/protesis/` carga
- [ ] Todas las imágenes se ven (abrir DevTools → Network, sin 404)
- [ ] WhatsApp link funciona (`+56944157542`)
- [ ] Meta OG image aparece al compartir (usar https://metatags.io)
- [ ] Mobile responsive (Chrome DevTools responsive mode)

## Nota sobre tracking
La landing actual no tiene GA4 ni Meta Pixel. Si la campaña la vas a correr en Meta Ads, agregar el pixel antes de desplegar.
