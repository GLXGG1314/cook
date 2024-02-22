# Copyright The OpenTelemetry Authors
# SPDX-License-Identifier: Apache-2.0

package(default_visibility = ["//visibility:public"])

cc_library(
    name = "headers",
    hdrs = glob(["include/**/*.h"]),
    strip_include_prefix = "include",
)
Language:        Cpp
BasedOnStyle:  Google
PointerAlignment: Left
Checks:          'clang-analyzer-*,readability-redundant-*,performance-*'
WarningsAsErrors: 'clang-analyzer-*,readability-redundant-*,performance-*'
HeaderFilterRegex: '.*'
AnalyzeTemporaryDtors: false
FormatStyle:     none
User:            user
