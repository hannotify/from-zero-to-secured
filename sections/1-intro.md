<!-- .slide: data-background-opacity="1.0" -->

## From Zero to Secured:
### Live-Coding a Full-Stack 
## Jakarta EE REST App 
#### with MicroProfile and JWT Authentication

<table>
    <tr>
        <td style="text-align: right; vertical-align: middle;" width="36%">Hanno Embregts</td>
        <td style="text-align: left; padding: 0 0 0 0; vertical-align: middle;">
            <img width="16%" data-src="img/logos/ace-pro-spade.png" class="no-background" style="margin-top: 30px; vertical-align: middle;"/>
            <img width="20%" data-src="img/logos/java-champion.png" class="no-background" style="margin-top: 30px; vertical-align: middle;"/>
        </td>
        <td style="vertical-align: middle; text-align: right;"><i class="fa-brands fa-bluesky" style="color: white"></i></td>
        <td style="vertical-align: middle; padding: 0 0 0 0"><a href="https://bsky.app/profile/hanno.codes">@hanno.codes</a></td>
    </tr>
</table>
<img width="10%" data-src="img/logos/jcon-2025.png" class="no-background"/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
<img width="10%" data-src="data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCAzMyAzMyIgc2hhcGUtcmVuZGVyaW5nPSJjcmlzcEVkZ2VzIj48cGF0aCBmaWxsPSIjZmZmZmZmIiBkPSJNMCAwaDMzdjMzSDB6Ii8+PHBhdGggc3Ryb2tlPSIjMDAwMDAwIiBkPSJNMiAyLjVoN20xIDBoM20zIDBoMW0yIDBoM20yIDBoN00yIDMuNWgxbTUgMGgxbTMgMGgybTEgMGgybTEgMGgzbTMgMGgxbTUgMGgxTTIgNC41aDFtMSAwaDNtMSAwaDFtMSAwaDFtMiAwaDNtMSAwaDFtMSAwaDFtMSAwaDFtMiAwaDFtMSAwaDNtMSAwaDFNMiA1LjVoMW0xIDBoM20xIDBoMW0zIDBoMW0xIDBoMW0xIDBoMW0xIDBoM20xIDBoMW0xIDBoMW0xIDBoM20xIDBoMU0yIDYuNWgxbTEgMGgzbTEgMGgxbTMgMGgybTEgMGgxbTMgMGgybTEgMGgxbTEgMGgxbTEgMGgzbTEgMGgxTTIgNy41aDFtNSAwaDFtMSAwaDFtMyAwaDNtMSAwaDFtNSAwaDFtNSAwaDFNMiA4LjVoN20xIDBoMW0xIDBoMW0xIDBoMW0xIDBoMW0xIDBoMW0xIDBoMW0xIDBoMW0xIDBoN00xMSA5LjVoMW0xIDBoMm0yIDBoMW0yIDBoM00yIDEwLjVoMW0xIDBoMW0zIDBoMm0xIDBoM20yIDBoMm0zIDBoMW0zIDBoMW0yIDBoMW0xIDBoMU0zIDExLjVoMW0yIDBoMm0yIDBoMW0yIDBoMm0xIDBoMm0yIDBoM20xIDBoMm0zIDBoMk0yIDEyLjVoMm0xIDBoMW0xIDBoMm0yIDBoMW0yIDBoMm0xIDBoMm0xIDBoMm01IDBoMm0xIDBoMU00IDEzLjVoMW0xIDBoMW0yIDBoMW0xIDBoMm0xIDBoMW0zIDBoMW0xIDBoMW0xIDBoMW00IDBoMU0yIDE0LjVoMW0yIDBoNG0yIDBoMW0yIDBoMm0xIDBoMm0yIDBoMm0xIDBoMW01IDBoMU0zIDE1LjVoMm0xIDBoMW0yIDBoMW0xIDBoMm0yIDBoMW0yIDBoMW0xIDBoMW0xIDBoMW0xIDBoMm0zIDBoMk0yIDE2LjVoMm0yIDBoMW0xIDBoMW0xIDBoMW0yIDBoMm0xIDBoMm0zIDBoMW0xIDBoMW0xIDBoMW00IDBoMU02IDE3LjVoMm0yIDBoMW01IDBoMW0zIDBoNG0xIDBoMk0zIDE4LjVoMm0xIDBoM20yIDBoMW0zIDBoNG0zIDBoNG00IDBoMU00IDE5LjVoMW00IDBoNG0xIDBoMm0yIDBoMm0xIDBoMm0xIDBoMW0zIDBoM00yIDIwLjVoMm0zIDBoMm0yIDBoMm00IDBoMW0yIDBoMm0zIDBoMW0xIDBoMW0yIDBoMU00IDIxLjVoMW0xIDBoMW0yIDBoMm0yIDBoM20xIDBoMW0yIDBoM20xIDBoMU0yIDIyLjVoN20yIDBoMW0zIDBoMW0xIDBoM20yIDBoNm0xIDBoMU0xMCAyMy41aDFtMyAwaDFtMyAwaDFtMyAwaDFtMyAwaDNtMSAwaDFNMiAyNC41aDdtMSAwaDNtMSAwaDZtMiAwaDFtMSAwaDFtMSAwaDFtMyAwaDFNMiAyNS41aDFtNSAwaDFtMiAwaDFtMiAwaDFtMSAwaDNtMyAwaDFtMyAwaDFNMiAyNi41aDFtMSAwaDNtMSAwaDFtMiAwaDJtMiAwaDRtMSAwaDhtMSAwaDFNMiAyNy41aDFtMSAwaDNtMSAwaDFtMyAwaDJtMSAwaDRtMSAwaDRtMSAwaDRtMSAwaDFNMiAyOC41aDFtMSAwaDNtMSAwaDFtMSAwaDJtMSAwaDFtMSAwaDFtMSAwaDFtNSAwaDFtMiAwaDFtMiAwaDJNMiAyOS41aDFtNSAwaDFtMiAwaDFtMSAwaDFtMSAwaDJtNSAwaDJtMSAwaDFtMSAwaDFNMiAzMC41aDdtMSAwaDJtMSAwaDJtMiAwaDFtMiAwaDFtMSAwaDVtMyAwaDEiLz48L3N2Zz4K" class="no-background">

---

<!-- .slide: data-background-color="black" data-background-image="img/background/checo-perez-racing-point.jpg" data-background-opacity="0.4" -->

# What is more important? <!-- .element class="stroke" -->

<blockquote class="explanation">
The journey or the destination?
</blockquote>

<https://commons.wikimedia.org/wiki/File:Sergio_Perez-Racing_Point_RP_20_%283%29.jpg> <!-- .element: class="attribution" -->
