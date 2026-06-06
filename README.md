[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/_Lc0okLm)
[![Open in Codespaces](https://classroom.github.com/assets/launch-codespace-2972f46106e565e64193e422d61a12cf1da4916b45550586e14ef0a7c637dd04.svg)](https://classroom.github.com/open-in-codespaces?assignment_repo_id=22907692)
# M2.3.2 Actividad Firmas digitales

---
## Crear llaves privadas y publicas con ssh-keygen
```bash
openssl genpkey -algorithm RSA -out privada.pem -aes256
```
> Te solicita una contraseña minima de 4 caracteres.

```bash
openssl rsa -in privada.pem -pubout -out publica.pem
```

---
## Firmar con openssl
Para firmar el archivo `texto.txt` con la llave privada `privada.pem` usando el algoritmo `sha256` dejando la firma en `texto.txt.sha256` 
```bash
openssl dgst -sha256 -sign privada.pem  -out texto.txt.sha256 texto.txt
```

## Verificar firma con openssl

```bash
openssl dgst -sha256 -verify publica.pem -signature texto.txt.sha256 texto.txt
```
o sin el algoritmo
```bash
openssl dgst -verify publica.pem -signature texto.txt.sha256 texto.txt
```

---
## Revisa y actualiza tus certificados en linux
los certificados de Autoridades Certificadora están en `/etc/ssl/certs`
```bash
ls /etc/ssl/certs/
```

para actualizar los certificados
```bash
$sudo update-ca-certificates -v
Updating certificates in /etc/ssl/certs...
0 added, 0 removed; done.
Running hooks in /etc/ca-certificates/update.d...
Processing triggers for ca-certificates-java (20230710~deb12u1) ...
done.
done.

```

en ocasiones e necesario refrescar los certificado por completo, con la opción `-f` es posible hacer esto.
```bash
sudo update-ca-certificates -f
```

---
## Firmas digitales de archivos en Windows
Los archivos se firman de manera digital para dar la seguridad que son de una fuente verificada, una vez en el equipo, se pueden observar las firmas en las propiedades del archivo, en una pestaña especial para este uso, Firmas digitales.

![alt text](images/Firma_digital_vmware_instalacion.png)

---

El botón de detalles verifica la firma con el certificado publico y el algoritmo con el que se firmo, esto para asegurar que el documento no se modifico en algún momento.

![alt text](images/firma_verificada_vmware.png)
---

![alt text](images/Certificado_de_la_firma_vmware.png)
---
El certificado es verificado por una Autoridad Certificadora (CA)

![alt text](images/certificado_vmware_path.png)


---
## Actividad Verificando firma de archivos

- Crea una llave privada
- Crea una llave publica con la privada
- Firma los documentos txt
- verifica la firma
- verifica la firma cruzando los archivos (firma1 con archivo2)