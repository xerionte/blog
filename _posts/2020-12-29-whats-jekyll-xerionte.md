---
layout: post
title:  ¿Y para qué este Blog? ¿Y por qué con Jekyll sobre Github?
---

[Jekyll](https://jekyllrb.com) es un generador de sitios web estáticos, una herramienta de código libre que permite crear websites complejos y flexibles de todos las formas y tamaños. Extraído de [the project's readme](https://github.com/mojombo/jekyll/blob/master/README.markdown):

  > Jekyll is a simple, blog aware, static site generator. It takes a template directory [...] and spits out a complete, static website suitable for serving with Apache or your favorite web server. This is also the engine behind GitHub Pages, which you can use to host your project’s page or blog right here from GitHub.

 Se trata de una herramienta muy útil que en mi caso estoy empleando con una apariencia y formato (Theme) denominado Lanyon. 
 
 A pesar de los cientos de blogs que puedas haber leído, no fué trivial montar sobre Github un blog que puedas editar y testar en tu equipo para luego subirlo cuando lo hayas revisado y validado a través de Jekyll. O al menos para mí, que no me dedico expresamente a la creación de infraestructuras de sitios web, aunque como soy informático lo mismo hago ésto, que cambio las pilas a las calculadoras.   

 Comencé mediante un *fork* del creador del Theme **Lanyon** y creé un sitio con la apariencia que mejor encaja con la estética barruntada, pero para un mejor control he preferido poder sincronizar los contenidos alojados en el site desde mi puesto de trabajo empleando la herramienta Github Desktop. Este requisito autoexigido, me obligó a realizar adaptaciones que retrasaron la puesta a punto de la creación de este blog. Vale, eso las obligaciones y la procrastinación. 
 
 Preferí penalizar la rapidez de la puesta en marcha que permite el propio site de Github por la posibilidad de comprobar antes la apariencia, en mi equipo local, de lo publicado y también por mantener una copia de los contenidos, para lo cual me he tenido que instalar en el puesto de trabajo MacBook Pro con OSX Big Sur (por cierto recién traído por Papá Noel),  
 
 * Homebrew, 
 * el paquete del compilador ruby, 
 * el paquete de Jekyll, 
 * así como los paquetes con las librerías y los gem de ruby necesarios. 
 * Ah! Y pelear con la configuración de  Github, que aunque es gratuita, no te ofrece la posibilidad de usar sus infraestructura de manera evidente para publicar el blog....
 
 Un consejo, es  emplear este enlace de [Nikhita](https://www.nikhita.dev/build-blog-using-github-jekyll) y sus referencias donde comenta detalladamente los pasos dados.
 
 Si en algún momento os planteis crear un blog o CMS de páginas estáticas con parecidos mimbres No os desaniméis, aunque al final deberéis ejecutar varias decenas de pruebas como ésta. Mucho ensayo y error, y bastantes lecturas *googleadas* regaladas por  distintos usuarios cuyas referencias han quedado en los históricos de los navegadores:
 
 {% highlight js %}
 
xerionte@MacBook-Pro ~ % ruby -v
ruby 2.7.2p137 (2020-10-01 revision 5445e04352) [x86_64-darwin20]
xerionte@MacBook-Pro ~ % gem install --user-install bundler jekyll
Fetching bundler-2.2.3.gem
WARNING:  You don't have /Users/xxxx/.gem/ruby/2.7.0/bin in your PATH,
	  gem executables will not run.
Successfully installed bundler-2.2.3
Parsing documentation for bundler-2.2.3
Installing ri documentation for bundler-2.2.3
Done installing documentation for bundler after 2 seconds
Fetching addressable-2.7.0.gem
Fetching colorator-1.1.0.gem
Fetching eventmachine-1.2.7.gem
Fetching http_parser.rb-0.6.0.gem
Fetching concurrent-ruby-1.1.7.gem
............
Fetching unicode-display_width-1.7.0.gem
Fetching jekyll-4.2.0.gem
Fetching terminal-table-2.0.0.gem
Successfully installed public_suffix-4.0.6
Successfully installed addressable-2.7.0
Successfully installed colorator-1.1.0
Building native extensions. This could take a while...
Successfully installed eventmachine-1.2.7
Building native extensions. This could take a while...
Successfully installed http_parser.rb-0.6.0
Successfully installed em-websocket-0.5.2
Successfully installed concurrent-ruby-1.1.7

HEADS UP! i18n 1.1 changed fallbacks to exclude default locale.
But that may break your application.

If you are upgrading your Rails application from an older version of Rails:

Please check your Rails app for 'config.i18n.fallbacks = true'.
If you're using I18n (>= 1.1.0) and Rails (< 5.2.2), this should be
'config.i18n.fallbacks = [I18n.default_locale]'.
If not, fallbacks will be broken in your app by I18n 1.1.x.

If you are starting a NEW Rails application, you can ignore this notice.

{% endhighlight %}
 
 En la pelea, durante la instalación se aprende mucho acerca del funcionamiento y las dependencias de los distintos archivos de configuración ( especial atención a _config.yml y gemfile, estilos *gems* ), pero finalmente me ha ayudado bastante este vídeo de [Webjeda.](http://youtube.com/watch?v=Whbs1UlPWtM)
     
Y sobre lo segundo... **¿Para qué este blog?**
 
 Pues sobre todo, como bitácora (lo habitual de un blog) para que no se me olviden algunos de los conocimientos que voy recogiendo y que ese señor alemán nos esconde... Y porque quizás alguna píldora de conocimiento de algún apartado expuesto puede ser útil también a cualquier otr@, al igual que otr@s me ha resuelto lo que describí someramente en los párrafos anteriores.
 
 Aquí intentaré ir subiendo anotaciones, sobre todo de cuestiones que me hayan ido llamando la atención relacionadas con tecnología, la Seguridad IT, retos de hacking, *WriteUps de CTFs*, y otras cuestiones que me entretienen y apasionan . No padezco de titulitis, pero como he deslizado académicamente soy informático  he realizado un máster de postgrado relacionado con la  Seguridad IT relacionado con ámbito y variados  cursos de ciberseguridad :-), aunque también pueda contener información interesante. 
 
 Agradecido si has llegado hasta aquí.
 
 @xerionte
 
 
 
 

