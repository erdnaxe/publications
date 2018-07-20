# Compile all Markdown files except README and LICENSE
SOURCES := $(filter-out README.md LICENCE.md index.md, $(wildcard *.md))

# Set targets
BUILD_DIR := build/
TARGETS_PDF := $(addprefix $(BUILD_DIR),$(SOURCES:.md=.pdf))
TARGETS_WEB := $(addprefix $(BUILD_DIR),$(SOURCES:.md=.html))

ASSETS_BUILD_DIR := $(BUILD_DIR)assets/
ASSETS := $(wildcard assets/*)
WEBFONTS := $(wildcard fonts/*-webfont.woff)
TARGET_ASSETS := $(addprefix $(BUILD_DIR),$(ASSETS:.pdf=.svg))
TARGET_ASSETS += $(addprefix $(BUILD_DIR),$(WEBFONTS))

# Change LaTeX engine and use custom header and font
PARAMETERS_PDF := --pdf-engine=xelatex
PARAMETERS_PDF += --include-in-header="include/header.tex"
PARAMETERS_PDF += -V mainfont:"texgyrepagella.otf" \
	-V 'mainfontoptions: Path = fonts/, \
		UprightFont = *-regular, \
		BoldFont = *-bold, \
		ItalicFont = *-italic, \
		BoldItalicFont = *-bolditalic' \
	-V mathfont:"texgyrepagella-math.otf" \
	-V 'mathfontoptions: Path = fonts/, \
	    math-style=french'

# HTML documents settings
PARAMETERS_WEB := -s -c "assets/layout.css" --katex --toc -N

# Licence documents
PARAMETERS_PDF += -V include-before:"\printlicence" 
PARAMETERS_WEB += -A include/footer.html -B include/header.html 

# Use PDF assets in LaTeX and SVG in HTML
PARAMETERS_PDF += --default-image-extension=pdf
PARAMETERS_WEB += --default-image-extension=svg

all: $(TARGETS_PDF) $(TARGETS_WEB) $(TARGET_ASSETS)

$(ASSETS_BUILD_DIR)%.svg: assets/%.pdf
	@echo "Converting $< to SVG..."
	@mkdir -p "$(ASSETS_BUILD_DIR)" # Make sure build dir exists
	@pdftocairo -svg "$<" "$@" # Generate SVG

$(ASSETS_BUILD_DIR)%.png: assets/%.png
	@mkdir -p "$(ASSETS_BUILD_DIR)" # Make sure build dir exists
	@cp "$<" "$@" # Copy PNG

$(ASSETS_BUILD_DIR)%.jpg: assets/%.jpg
	@mkdir -p "$(ASSETS_BUILD_DIR)" # Make sure build dir exists
	@cp "$<" "$@" # Copy JPG

$(ASSETS_BUILD_DIR)%.css: assets/%.css
	@mkdir -p "$(BUILD_DIR)" # Make sure build dir exists
	@cp "$<" "$@" # Copy CSS

$(BUILD_DIR)fonts/%.woff: fonts/%.woff
	@mkdir -p "$(BUILD_DIR)fonts" # Make sure build dir exists
	@cp "$<" "$@" # Copy fonts

$(BUILD_DIR)%.pdf : %.md $(ASSETS) include/header.tex
	@echo "Generating $@..."
	@mkdir -p "$(BUILD_DIR)" # Make sure build dir exists
	@pandoc $(PARAMETERS_PDF) "$<" -o "$@"

$(BUILD_DIR)%.html : %.md include/footer.html include/header.html $(TARGET_ASSETS)
	@echo "Generating $@..."
	@mkdir -p "$(BUILD_DIR)" # Make sure build dir exists
	@pandoc $(PARAMETERS_WEB) "$<" -o "$@"

clean:
	@rm -rf $(TARGETS_PDF) $(TARGETS_WEB) $(TARGET_ASSETS)

