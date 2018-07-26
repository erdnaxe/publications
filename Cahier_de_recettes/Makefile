# Markdown list ordered
SOURCES := sauces.md

# Set target
BUILD_DIR := build/
TARGET_PDF := $(BUILD_DIR)index.pdf
TARGET_WEB := $(BUILD_DIR)index.html

ASSETS_BUILD_DIR := $(BUILD_DIR)assets/
ASSETS := $(wildcard assets/*)
WEBFONTS := $(wildcard fonts/*-webfont.woff)
TARGET_ASSETS := $(addprefix $(BUILD_DIR),$(ASSETS:.pdf=.svg))
TARGET_ASSETS += $(addprefix $(BUILD_DIR),$(WEBFONTS))

# Change LaTeX engine and use custom header and font
PARAMETERS_PDF := --pdf-engine=xelatex
PARAMETERS_PDF += --include-in-header="include/header.tex"
PARAMETERS_PDF += -V mainfont:"texgyrebonum.otf" \
	-V 'mainfontoptions: Path = fonts/, \
		UprightFont = *-regular, \
		BoldFont = *-bold, \
		ItalicFont = *-italic, \
		BoldItalicFont = *-bolditalic'

# HTML documents settings
PARAMETERS_WEB := -s -c "assets/layout.css" --toc

# Licence documents
PARAMETERS_PDF += -V include-before:"\printlicence" 
PARAMETERS_WEB += -A include/footer.html -B include/header.html 

# Use PDF assets in LaTeX and SVG in HTML
PARAMETERS_PDF += --default-image-extension=pdf
PARAMETERS_WEB += --default-image-extension=svg

all: $(TARGET_PDF) $(TARGET_WEB) $(TARGET_ASSETS)

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
	@mkdir -p "$(ASSETS_BUILD_DIR)" # Make sure build dir exists
	@cp "$<" "$@" # Copy CSS

$(BUILD_DIR)fonts/%.woff: fonts/%.woff
	@mkdir -p "$(BUILD_DIR)fonts" # Make sure build dir exists
	@cp "$<" "$@" # Copy fonts

$(BUILD_DIR)index.pdf : $(SOURCES) $(ASSETS) include/header.tex
	@echo "Generating $@..."
	@mkdir -p "$(BUILD_DIR)" # Make sure build dir exists
	@pandoc $(PARAMETERS_PDF) index.md $(SOURCES) -o "$@"

$(BUILD_DIR)index.html : $(SOURCES) $(ASSETS) include/footer.html include/header.html
	@echo "Generating $@..."
	@mkdir -p "$(BUILD_DIR)" # Make sure build dir exists
	@pandoc $(PARAMETERS_WEB) index.md $(SOURCES) -o "$@"

clean:
	@rm -rf $(TARGET_PDF) $(TARGET_WEB) $(TARGET_ASSETS)

