Using gettext with rebar

I've modified gettext to set  default values in de parse_transform compiler function and allow to use it with rebar. For some reason I couldn't make it work with environment variables.

The default values are:

* GETTEXT_TMP_NAME = "default"
* GETTEXT_DIR = "i18n"
* GETTEXT_DEF_LANG = os:getenv("LANG")

To compile the source code with rebar and use the gettext extension to generate de po file you must add [gettext] option to compiler options in rebar.config:

{erl_opts,[gettext,debug_info]}.

After running rebar compile a dets file appears in PROJECT_DIR/i18n/default/epot.dets, to extract the po file you must run  the command "erl -noshell -pa deps/gettext/ebin -s gettext_compile epot2po" or add it to a Makefile.  The po file appears in PROJECT_DIR/i18n/default/${LANG}/gettext.po

In test dir of this project you can find a complete example.