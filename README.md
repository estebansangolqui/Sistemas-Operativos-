# Sistemas-Operativos-
Practica

\documentclass[12pt,a4paper]{article}

\usepackage[spanish]{babel}
\usepackage[utf8]{inputenc}
\usepackage{graphicx}
\usepackage{geometry}
\usepackage{xcolor}
\usepackage{listings}
\usepackage{hyperref}

\geometry{margin=2.5cm}

\title{\textbf{Práctica 3: La línea de comando para levantar servicios en red}}
\author{Esteban Sangolqui}
\date{Noviembre de 2026}

\begin{document}

\maketitle

\section{Objetivo}

Configurar servicios de red en CentOS Stream,
implementando servidores FTP, HTTP, NTP y SSH,
aplicando medidas de seguridad mediante Firewalld
y SELinux.

\section{Materiales}

\begin{itemize}
    \item Computadora.
    \item Oracle VirtualBox.
    \item Máquina virtual CentOS Stream.
    \item MobaXterm.
    \item Conexión a Internet.
    \item Cuenta de GitHub.
\end{itemize}

\section{Procedimiento}

\subsection{Paso 1. Preparación de CentOS}

1. Abrir VirtualBox e iniciar la máquina virtual CentOS.

2. Configurar el adaptador de red en modo puente (Bridge).

3. Abrir la terminal y comprobar la versión:

\begin{verbatim}
cat /etc/centos-release
\end{verbatim}

4. Consultar la dirección IP:

\begin{verbatim}
ip addr
\end{verbatim}

5. Comprobar la conexión a Internet:

\begin{verbatim}
ping -c 4 google.com
\end{verbatim}

\subsection{Paso 2. Configuración del servidor FTP}

1. Instalar el servicio VSFTPD:

\begin{verbatim}
sudo dnf install vsftpd -y
\end{verbatim}

2. Habilitar e iniciar el servicio:

\begin{verbatim}
sudo systemctl enable --now vsftpd
\end{verbatim}

3. Crear un usuario restringido:

\begin{verbatim}
sudo useradd -s /sbin/nologin ftp_estudiante
\end{verbatim}

4. Asignar una contraseña:

\begin{verbatim}
sudo passwd ftp_estudiante
\end{verbatim}

5. Editar la configuración:

\begin{verbatim}
sudo nano /etc/vsftpd/vsftpd.conf
\end{verbatim}

6. Configurar el acceso FTP local y las opciones
de transferencia según los requisitos de la práctica.

7. Reiniciar el servicio:

\begin{verbatim}
sudo systemctl restart vsftpd
\end{verbatim}

8. Comprobar el funcionamiento:

\begin{verbatim}
sudo systemctl status vsftpd
\end{verbatim}

9. Probar la conexión y transferencia mediante
MobaXterm.

\subsection{Paso 3. Configuración del servidor HTTP}

1. Instalar Apache:

\begin{verbatim}
sudo dnf install httpd -y
\end{verbatim}

2. Habilitar e iniciar el servicio:

\begin{verbatim}
sudo systemctl enable --now httpd
\end{verbatim}

3. Ingresar al directorio web:

\begin{verbatim}
cd /var/www/html
\end{verbatim}

4. Editar la página principal:

\begin{verbatim}
sudo nano /var/www/html/index.html
\end{verbatim}

5. Incorporar nombres, apellidos e imágenes
en la página web.

6. Establecer los permisos de lectura:

\begin{verbatim}
sudo chmod 644 /var/www/html/index.html
\end{verbatim}

7. Configurar el acceso HTTP en el firewall:

\begin{verbatim}
sudo firewall-cmd --permanent --add-service=http
sudo firewall-cmd --reload
\end{verbatim}

8. Comprobar el servicio:

\begin{verbatim}
sudo systemctl status httpd
\end{verbatim}

9. Abrir el navegador e ingresar la dirección IP
del servidor para visualizar la página.

\subsection{Paso 4. Configuración del servidor NTP}

1. Instalar Chrony:

\begin{verbatim}
sudo dnf install chrony -y
\end{verbatim}

2. Habilitar e iniciar el servicio:

\begin{verbatim}
sudo systemctl enable --now chronyd
\end{verbatim}

3. Editar el archivo de configuración:

\begin{verbatim}
sudo nano /etc/chrony.conf
\end{verbatim}

4. Configurar los parámetros de sincronización
y acceso de red local según la práctica.

5. Reiniciar el servicio:

\begin{verbatim}
sudo systemctl restart chronyd
\end{verbatim}

6. Verificar la sincronización horaria:

\begin{verbatim}
chronyc tracking
chronyc sources -v
\end{verbatim}

7. Realizar la prueba de sincronización entre
Windows y CentOS.

\subsection{Paso 5. Configuración del servicio SSH}

1. Instalar el servidor SSH:

\begin{verbatim}
sudo dnf install openssh-server -y
\end{verbatim}

2. Habilitar e iniciar el servicio:

\begin{verbatim}
sudo systemctl enable --now sshd
\end{verbatim}

3. Permitir SSH en el firewall:

\begin{verbatim}
sudo firewall-cmd --permanent --add-service=ssh
sudo firewall-cmd --reload
\end{verbatim}

4. Consultar la dirección IP:

\begin{verbatim}
ip addr
\end{verbatim}

5. Abrir MobaXterm desde Windows.

6. Crear una sesión SSH utilizando la dirección IP
de CentOS, el usuario y su contraseña.

7. Comprobar que se puede acceder remotamente
a la terminal del servidor.

\subsection{Paso 6. Verificación de seguridad}

1. Comprobar el estado del firewall:

\begin{verbatim}
sudo firewall-cmd --state
sudo firewall-cmd --list-all
\end{verbatim}

2. Comprobar el estado de SELinux:

\begin{verbatim}
getenforce
\end{verbatim}

3. Verificar los servicios:

\begin{verbatim}
sudo systemctl status vsftpd
sudo systemctl status httpd
sudo systemctl status chronyd
sudo systemctl status sshd
\end{verbatim}

\section{Conclusiones}

Durante esta práctica se busca adquirir
conocimientos sobre la instalación y configuración
de servicios de red en CentOS Stream.

Además, se comprende la importancia de utilizar
herramientas de seguridad como Firewalld y SELinux
para proteger los servicios implementados.

\end{document}
