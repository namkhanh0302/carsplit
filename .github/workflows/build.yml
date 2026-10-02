name: Build CarSplit

on:
  workflow_dispatch:
  push:

jobs:
  build:
    runs-on: macos-latest
    steps:
      - uses: actions/checkout@v4

      - name: Install tools
        run: brew install ldid dpkg make

      - name: Install Theos
        run: |
          git clone --recursive https://github.com/theos/theos.git $HOME/theos
          git clone --depth=1 https://github.com/theos/sdks.git /tmp/sdks
          cp -R /tmp/sdks/*.sdk $HOME/theos/sdks/

      - name: Build
        run: |
          unzip -o CarSplit.zip
          cd CarSplit
          export THEOS=$HOME/theos
          export PATH="$(brew --prefix make)/libexec/gnubin:$PATH"
          make package

      - name: Upload deb
        uses: actions/upload-artifact@v4
        with:
          name: CarSplit-deb
          path: CarSplit/packages/*.deb
