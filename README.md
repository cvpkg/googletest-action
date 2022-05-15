# googletest-action

Install googletest on Github Actions, provided as re-usable "configure-build-install-export-import" steps.

## Use in workflows yml
action.yml:
```yml
- name: Install googletest
  uses: cvpkg/googletest-action@v0.1
  with:
    googletest_tag: 'release-1.11.0' # default is 'v1.11.0'
    # an env var 'googletest_tag' will be defined.
```

## Use in CMakeLists.txt
To set the correct paths, you could add to your `CMakeLists.txt`:
```cmake
if(DEFINED ENV{GITHUB_ACTIONS} AND DEFINED ENV{GITHUB_WORKSPACE})
  set(ARTIFACTS_DIR "$ENV{GITHUB_WORKSPACE}/artifacts")
  if(CMAKE_SYSTEM_NAME MATCHES "Windows")
    set(GTest_DIR "${ARTIFACTS_DIR}/googletest/$ENV{googletest_tag}/windows-x64/lib/cmake/GTest")
  elseif(CMAKE_SYSTEM_NAME MATCHES "Linux")
    set(GTest_DIR "${ARTIFACTS_DIR}/googletest/$ENV{googletest_tag}/linux-x64/lib/cmake/GTest")
  elseif(CMAKE_SYSTEM_NAME MATCHES "Darwin")
    set(GTest_DIR "${ARTIFACTS_DIR}/googletest/$ENV{googletest_tag}/mac-x64/lib/cmake/GTest")
  endif()
  find_package(GTest REQUIRED)
endif()
```

## References
- [googletest](https://github.com/google/googletest)