#
# Makefile
#
# Version:	$Id: Makefile,v 1.11 2006/09/21 23:17:42 aland Exp $
#

#
#  Note that "attributes.html" and "index.html" were hacked by hand
#  after running these Makefiles..
#
# $ grep H3 attributes.html | perl -ne 's:<H3>(\w)</H3>:<A HREF="#$1">$1</A> :;print' > attr-refs
# $ cat attributes.html | perl -pe 's:<H3>(\w)</H3>:<H3><A NAME="$1">$1</A></H3>:' > foo
# $ mv foo attributes.html
# $ chmod a+x attributes.html
#
# --- edit to add header/footer, CSS, and attr-refs from above.


RFC	= rfc2548.txt rfc2865.txt rfc2866.txt rfc2867.txt rfc2868.txt \
	  rfc2869.txt rfc3162.txt rfc3579.txt rfc3580.txt \
	  rfc4590.txt rfc4818.txt rfc4849.txt rfc5090.txt rfc5176.txt \
	  rfc5607.txt rfc5904.txt rfc6519.txt rfc6572.txt rfc6911.txt \
	  rfc6929.txt rfc6930.txt

HTML	= $(RFC:.txt=.html)

ATTRS	= $(addprefix attributes-,$(HTML));


all:

git-add: $(RFC) $(HTML) $(ATTRS)
	@git add $^

index.html: html
	./update.sh

refs: $(RFC)
	@./genref.pl $(RFC) > refs
	@echo 'rfc2865 Class' >> refs
	@echo 'rfc2865 State' >> refs
	@echo 'rfc4818 Delegated-IPv6-Prefix' >> refs

letters.html: refs genletters.pl
	@./genletters.pl < $^ > $@

clean:
	rm -f refs *rfc*.html *~ index.html

html: $(HTML)

%.html: %.txt refs rewrite.pl per-rfc.pl
	@./rewrite.pl $<
	@./per-rfc.pl $<

.PHONY: all clean install html
