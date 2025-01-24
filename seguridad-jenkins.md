# 📌 Seguridad en Jenkins.
Jenkins es una herramienta importante en el ecosistema de una empresa de desarrollo y para protegerla existen unas practicas llamadas 'buenos habitos' que son las siguientes:

**¿Por qué es importante la seguridad en Jenkins?**   
<span style="color:red;" >En pasado se han descubierto brechas de seguridad que pueden ser explotadas sin la necesidad de iniciar sesión en Jenkins. Esto otorgó acceso a una importante cantidad de información sensible a usuarios malintencionados.  </span>




### 🔸 Proteger Jenkins de internet.
**Jenkins es una herramienta de uso interno en red privada.** Para proteger a Jenkins de la wlan podemos crear reglas en el cortafuegos y ubicarlo tras una VPN empresarial. En caso de que esté en la nube, utilizar el firewall que ofrecen y bloquear todos los puertos, 
permitiendo el acceso solo a la IP del a oficina o la VPN de disponer de una. 

>[!CAUTION]
>Recuerda agregar a la listablanca o whitelist de tu cortafuegos las direcciones de **github**, **gitlab** y **bitbucket** para que Jenkins pueda hacer *pull* de los repositorios de trabajo.
    
### 🔸 
