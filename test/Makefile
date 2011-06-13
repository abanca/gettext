ERL			?= erl
ERL			= erlc
EBIN_DIRS		:= $(wildcard deps/*/ebin)

.PHONY: rel deps test

all: deps compile

compile: deps
	@./rebar compile

deps:
	@./rebar get-deps
	@./rebar check-deps

console:
	@erl -pa deps/*/ebin  ebin  
	
clean:
	@./rebar clean
	@rm -rf i18n

realclean: clean
	@./rebar delete-deps

test:
	@./rebar skip_deps=true ct

eunit:
	@./rebar skip_deps=true eunit

analyze: checkplt
	@./rebar skip_deps=true dialyze

buildplt:
	@./rebar skip_deps=true build-plt

checkplt: buildplt
	@./rebar skip_deps=true check-plt

xref:
	@./rebar skip_deps=true xref

gettext:
	@erl -noshell -pa deps/gettext/ebin -s gettext_compile epot2po
	
	
	