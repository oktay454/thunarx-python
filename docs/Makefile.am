docsdir = $(docdir)

BUILDDIR = $(top_builddir)/docs

REF_VERSION = $(VERSION)
FULL_VERSION = $(VERSION)

HTML_STYLE = $(PYGOBJECT_DATADIR)/pygobject/xsl/ref-html-style.xsl
PDF_STYLE = $(PYGOBJECT_DATADIR)/pygobject/xsl/pdf-style.xsl

XMLFILES = 							\
	reference/thunarx-python-ref.xml			\
	reference/thunarx-python-overview.xml			\
	reference/thunarx-python-overview-example.xml			\
	reference/thunarx-python-class-reference.xml			\
	reference/thunarx-python-provider-reference.xml			\
	reference/thunarx-python-menu-provider.xml \
	reference/thunarx-python-property-page.xml \
	reference/thunarx-python-property-page-provider.xml \
	reference/thunarx-python-renamer.xml \
	reference/thunarx-python-renamer-provider.xml \
	reference/thunarx-python-preferences-provider.xml \
	reference/thunarx-python-file-info.xml

HTMLdir = $(datadir)/gtk-doc/html/thunarx-python
HTMLFILES =						\
	html/index.html					\
	html/index.sgml					\
	html/thunarx-python-overview.html \
	html/thunarx-python-overview-example.html \
	html/thunarx-python-class-reference.html \
	html/thunarx-python-provider-reference.html \
	html/class-thunarx-python-menu-provider.html  \
	html/class-thunarx-python-property-page.html  \
	html/class-thunarx-python-property-page-provider.html  \
	html/class-thunarx-python-renamer.html  \
	html/class-thunarx-python-renamer-provider.html  \
	html/class-thunarx-python-preferences-provider.html  \
	html/class-thunarx-python-file-info.html  \
	html/thunarx-python.devhelp

CSS_FILES = $(PYGOBJECT_PYGDOCS)/style.css
CSSdir = $(HTMLdir)
CSS_DATA = $(CSS_FILES)

BUILT_SOURCES = 		\
	reference/builddate.xml	\
	$(HTMLFILES)

CLEANFILES = 			\
	thunarx-python-ref.*	\
	reference/builddate.xml \
	$(HTMLFILES)

EXTRA_DIST = 		\
	$(XMLFILES) 

REFERENCE_DEPS = 	\
	reference 	\
	$(XMLFILES)

if ENABLE_GTK_DOC

reference/builddate.xml: $(REFERENCE_DEPS)
	$(PYTHON) -c 'import datetime; print datetime.date.today()' > $@

$(HTMLFILES): $(REFERENCE_DEPS) reference/builddate.xml
	xsltproc --nonet --xinclude -o $(BUILDDIR)/html/ \
		 --path $(BUILDDIR)/reference:$(srcdir)/reference \
		 --stringparam gtkdoc.bookname "thunarx-python" \
		 --stringparam gtkdoc.version ${REF_VERSION} \
		 $(HTML_STYLE) $(srcdir)/reference/thunarx-python-ref.xml
	$(PYGOBJECT_FIXXREF) -i $(PYGOBJECT_PYGDOCS) $(BUILDDIR)/html 
	touch $@

pdf: $(REFERENCE_DEPS) reference/builddate.xml
	xsltproc --nonet --xinclude -o thunarx-python-ref.fo \
		$(PDF_STYLE) reference/thunarx-python-ref.xml
	pdfxmltex thunarx-python-ref.fo >output </dev/null
endif
