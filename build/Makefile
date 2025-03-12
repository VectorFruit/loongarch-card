TARGETS := lacard

.PHONY: all $(TARGETS) clean docker

all: $(TARGETS)

docker:
	cd .. && docker run -it -v .:/build riscvintl/riscv-docs-base-container-image:latest /bin/sh -c 'cd ./build; make'

ASCIIDOCTOR_OPTS := \
  -a compress \
  --attribute=mathematical-format=svg \
  --failure-level=ERROR \
  --require=asciidoctor-diagram \
  --require=asciidoctor-mathematical \
  -a scripts=cjk \
  --trace

SRCDIR := ../src

lacard: loongarch-card.pdf

loongarch-card.pdf: $(SRCDIR)/loongarch-card.adoc
	@echo "Building Loongarch Card"
	asciidoctor-pdf $(ASCIIDOCTOR_OPTS) \
	  --out-file=$@.tmp $<
	@mv $@.tmp $@

clean:
	rm -f loongarch-card.pdf
	rm -f *.svg
