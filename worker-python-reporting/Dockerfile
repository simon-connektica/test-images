# Why Debian: https://pythonspeed.com/articles/alpine-docker-python/
# Cannot use 'slim-bookworm' because latex requires a full Debian image.
FROM python:3.11-bookworm

RUN apt-get update && apt-get install -y \
    ca-certificates curl wget && \
    rm -rf /var/cache/apt/lists

# asciidoctor + asciidoctor-pdf
RUN apt-get update && apt-get install -y \
    asciidoctor \
    ruby-asciidoctor-pdf \
    ruby-rouge && \
    rm -rf /var/cache/apt/lists

# LaTeX + pdflatex
RUN wget https://mirror.ctan.org/systems/texlive/tlnet/install-tl-unx.tar.gz \
    && mkdir /install-tl-unx \
    && tar -xvf install-tl-unx.tar.gz -C /install-tl-unx --strip-components=1 \
    && echo "selected_scheme scheme-basic" >> /install-tl-unx/texlive.profile \
    && sed -i 's/no-check-certificates/no-check-certificate/g' /install-tl-unx/tlpkg/TeXLive/TLConfig.pm \
    && /install-tl-unx/install-tl -profile /install-tl-unx/texlive.profile \
    && rm -r /install-tl-unx \
    && rm install-tl-unx.tar.gz

ENV PATH="/usr/local/texlive/2023/bin/x86_64-linux:${PATH}"
ENV MANPATH="/usr/local/texlive/2023/texmf-dist/doc/man"
ENV INFOPATH="/usr/local/texlive/2023/texmf-dist/doc/info"

# Install latex packages
RUN tlmgr install latexmk \
    adjustbox \
    xcolor  \
    xkeyval \
    collectbox \
    booktabs \
    multirow \
    datetime \
    etoolbox \
    fmtcount \
    caption \
    helvetic \
    titlesec \
    tocloft

RUN pip install poetry==1.6.1
