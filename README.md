# A simple skbuild example
Please use python command to create a virtual environment and inspect the site-packages in the virtual environment to see how the targets are installed.

```bash
python3 -m venv venv
source venv/bin/activate
pip install .
```

After that, you will see
- install_folder_for_inspect/mytest/lib/libwithprefix.{dylib,so}: 
This is because `cpp_src/using_prefix/CMakeLists.txt` has a line `LIBRARY DESTINATION ${CMAKE_INSTALL_PREFIX}/${EXAMPLE_RELATIVE_LOCATION}/lib` that explicitly specifies the prefix at the configuration time.
- venv/lib/python3.xx/site-packages/mytest/noprefix.cpython-3xx-{darwin,x64,...}.so:
This is because `cpp_src/not_using_prefix/CMakeLists.txt` has a line `LIBRARY DESTINATION ${EXAMPLE_RELATIVE_LOCATION}` that specifies a relative path relative to the install prefix. However, the install prefix is changed between cmake-configuration phase and make-install phase. The target .so file is then installed into the changed install prefix location.
- venv/lib/python3.xx/site-packages/mytest/libsomeprecompiled.so:
This is because of the `cpp_src/pre_compiled_artifacts/CMakeLists.txt` has a line `install(FILES ${libname} DESTINATION ${EXAMPLE_RELATIVE_LOCATION})` that install this pre-compiled file to the relative location. The relative location follows the rules in the previous case where the changing install prefix will apply to pre-compiled file.
- venv/lib/python3.xx/site-packages/skbuild_prefix_example-0.1.0.dist-info/RECORD:
In the record, all the files installed with relative location will be recorded here, including the pre-compiled files if they are put into this place by install command. 

Notes:
- If the precompiled files are put into site-packages/ via file() in cmake, they will not appear in the RECORD. This is because they did not follow the installation, therefore never appearing in the scikit-build-core's temporary installation location. Note that I mentioned earlier that the install prefix changes between cmake-configuration phase and make-install phase. The scikit-build-core's temporary installation location is applied in the make-install phase.
