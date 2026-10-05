Here you can find my CV and my publication record.

{% assign cv_pdf = site.static_files | where: "path", "/files/CV_Bortolas.pdf" | first %}
<ul class="feature-icons">
{% if cv_pdf %}<li class="icon solid fa-file-alt"><a href="files/CV_Bortolas.pdf">Curriculum Vitae</a></li>{% endif %}
<li class="icon solid fa-book"><a href="https://ui.adsabs.harvard.edu/search/q=author%3A%22Bortolas%2C%20E.%22&amp;sort=date%20desc%2C%20bibcode%20desc">Publications (ADS)</a></li>
<li class="icon solid fa-scroll"><a href="https://arxiv.org/search/?query=Bortolas%2C+E&amp;searchtype=author&amp;order=-announced_date_first">Preprints (arXiv)</a></li>
<li class="icon brands fa-orcid"><a href="https://orcid.org/0000-0001-9458-821X">ORCID</a></li>
</ul>
