# Migración de WordPress Local a Hosting Real

**Autor:** Jose  
**Módulo:** IAW - Implantación de Aplicaciones Web  

---

## Pasos para migrar WordPress

### 1. Exportar la base de datos
- Abre `http://localhost/phpmyadmin`
- Selecciona la base de datos de WordPress
- Pestaña **Exportar** → formato SQL → **Continuar**
- Se descarga un archivo `.sql`

### 2. Comprimir los archivos de WordPress
- Ve a `C:\xampp\htdocs\wp_ex\`
- Selecciona todo → clic derecho → **Comprimir en ZIP**

### 3. Contratar un hosting
- Contrata un hosting con PHP y MySQL (ej: Hostinger, InfinityFree)
- Crea una base de datos MySQL desde el panel del hosting
- Anota: nombre BD, usuario y contraseña

### 4. Subir los archivos
- Abre **FileZilla** y conéctate al hosting con los datos FTP
- Sube el ZIP a la carpeta `public_html` y extráelo

### 5. Importar la base de datos
- Accede al phpMyAdmin del hosting
- Selecciona tu base de datos → pestaña **Importar**
- Sube el archivo `.sql` exportado antes

### 6. Editar wp-config.php
Cambia los datos de conexión por los del hosting:
```php
define( 'DB_NAME',     'nombre_bd' );
define( 'DB_USER',     'usuario_bd' );
define( 'DB_PASSWORD', 'contraseña' );
define( 'DB_HOST',     'localhost' );
```

### 7. Actualizar las URLs
En el phpMyAdmin del hosting ejecuta:
```sql
UPDATE wp_options 
SET option_value = 'https://tudominio.com' 
WHERE option_name = 'siteurl' OR option_name = 'home';
```

### 8. Verificar
- Abre `https://tudominio.com` → debe cargar WordPress
- Abre `https://tudominio.com/wp-admin` → debe cargar el panel
