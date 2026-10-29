# 第三方组件与许可范围

Apache-2.0 只覆盖本项目按该许可提供的代码和文档，不覆盖所有第三方素材或商标。NOTICE 不修改 LICENSE。GUI 没有包含 Python 运行时；CLI 独立包包含 CPython 3.13.9、选定标准库/扩展模块、PyInstaller 引导部分及预编译项目后端。详细原始条款见 CLI 包内或本目录 licenses/，相应组件仍依各自许可。没有声明这些第三方拥有者为本项目担保。

# Third-party notices — GUI

VoiceDraft project code and documentation are licensed under Apache-2.0; see LICENSE and NOTICE. Individual contribution copyrights remain with their respective rightsholders. This does not relicense Apple frameworks, symbols or trademarks.

The GUI uses macOS AppKit, SwiftUI, AVFoundation, Speech, ApplicationServices and Carbon APIs supplied by the operating system. The inspected App contains project executables, configuration, signature data and localized strings; no separate Apple framework/font/symbol asset library is redistributed in this package. SF Symbols (including waveform.circle.fill and mic.circle) are referenced through system APIs for display on macOS, not provided as reusable artwork under Apache-2.0. Apple system/software agreements and symbol restrictions remain applicable. This is not an Apple endorsed product; Apple trademarks do not imply affiliation.

Python and Xcode are development tools for this GUI source tree, not included runtime dependencies in the GUI App-only distribution. The CLI package separately bundles CPython/PyInstaller runtime components and carries its own licenses; see the public third-party overview for that product.

Sources: https://developer.apple.com/sf-symbols/ and https://developer.apple.com/design/human-interface-guidelines/sf-symbols . Availability of an API or asset is not a complete legal clearance of every intended reuse; exported artwork, branding or new third-party assets require separate review.

# Third-party runtime notices

VoiceDraft code is distributed under Apache License2.0 (LICENSE). Source code is temporarily kept in private repositories; that does not add restrictions to rights granted by this license.

This standalone package embeds CPython3.13 and its standard library. See licenses/CPython-3.13.txt and CPython-Third-Party-Notices.html for PSF and incorporated component notices, including OpenSSL/expat/libffi/zlib where applicable. The HTML is the matching Python distribution's license documentation and remains readable without its stylesheet.

The executable is assembled with PyInstaller6.22.3. See its COPYING notice, including the bootloader exception. Notices for its build-time helpers are also retained as attribution; retaining a notice does not imply every such tool runs in the installed application.

Apple system frameworks are used from the target OS; they are not copied into this package. The two VoiceDraft native executables are existing precompiled project backends. No third-party source ownership or license is transferred by the packaging operation.

## Runtime redistribution and project scope

Apache-2.0 applies to project code/documentation, not blanket ownership of CPython, OpenSSL, expat, zlib, liblzma or Apple assets. Individual upstream copyright notices and applicable terms remain in the supplied notices. CPython is redistributed as a subset with the interpreter framework, selected extension modules and standard-library bytecode relocated for this application; PyInstaller adjusts packaging/load locations. This is not an assertion that upstream Python source was patched or that the full upstream distribution is included. The supplied Python license documentation is from the matching local 3.13.9 distribution; the current online 3.13 documentation may describe a newer patch release.

The inspected _lzma extension statically incorporates liblzma (5.2.3 version strings observed); the upstream XZ 5.2.3 COPYING places liblzma source in the public domain and warns that compiler-added code can carry separate terms. See licenses/XZ-LIBLZMA-NOTICE.md. _bz2 links to macOS /usr/lib/libbz2; that system library is not copied into this package. libssl.3.dylib/libcrypto.3.dylib are bundled; OpenSSL 3.0 license material is retained in the Python incorporated-software notices (Apache-2.0). Python's incorporated components also retain their specific notices. No full XZ command-line suite, Tcl/Tk framework or compiler is bundled.

Apple system symbols in the project UI are requested through system APIs for macOS display; no separately exported symbol pack is licensed under Apache-2.0. System software, symbols and marks remain subject to Apple's applicable terms. No Apple, Python or PyInstaller endorsement is claimed. This inspection is not a complete supply-chain or legal audit.

Sources: https://docs.python.org/3.13/license.html ; https://pyinstaller.org/en/stable/license.html ; https://raw.githubusercontent.com/tukaani-project/xz/v5.2.3/COPYING ; https://developer.apple.com/sf-symbols/ .
