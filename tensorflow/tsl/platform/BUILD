# Description:
#   Tensor Standard Libraries.
#
#   The libraries in this package are not allowed to have ANY dependencies
#   to other TF components outside of TSL.

# buildifier: disable=same-origin-load
load("@bazel_skylib//lib:selects.bzl", "selects")
load("//tensorflow:tensorflow.bzl", "get_compatible_with_portable")
load(
    "//tensorflow:tensorflow.bzl",
    "tf_cc_test",
    "tf_copts",
    "tf_cuda_library",
)
load(
    "//tensorflow/core/platform:build_config.bzl",
    "tf_cuda_libdevice_path_deps",
    "tf_fingerprint_deps",
    "tf_google_mobile_srcs_no_runtime",
    "tf_logging_deps",
    "tf_platform_deps",
    "tf_protobuf_compiler_deps",
    "tf_protobuf_deps",
    "tf_resource_deps",
    "tf_testing_deps",
    "tf_windows_aware_platform_deps",
)
load(
    "//tensorflow/core/platform:rules_cc.bzl",
    "cc_library",
)

package(
    default_visibility = [
        "//visibility:public",
    ],
    licenses = ["notice"],
)

exports_files(
    [
        "mutex.h",
        "stringpiece_test.cc",
    ],
    visibility = [
        "//tensorflow/core/platform:__subpackages__",
        "//tensorflow/tsl:__subpackages__",
    ],
)

cc_library(
    name = "base64",
    srcs = ["base64.cc"],
    hdrs = ["base64.h"],
    deps = [
        ":errors",
        ":status",
        ":stringpiece",
    ],
)

cc_library(
    name = "blocking_counter",
    hdrs = ["blocking_counter.h"],
    deps = [
        ":logging",
        ":mutex",
    ],
)

cc_library(
    name = "byte_order",
    hdrs = ["byte_order.h"],
    compatible_with = get_compatible_with_portable(),
)

cc_library(
    name = "coding",
    srcs = ["coding.cc"],
    hdrs = ["coding.h"],
    deps = [
        ":byte_order",
        ":stringpiece",
        ":types",
    ],
)

cc_library(
    name = "denormal",
    srcs = ["denormal.cc"],
    hdrs = ["denormal.h"],
    deps = [
        ":macros",
        ":platform",
        ":platform_port",
    ],
)

tf_cc_test(
    name = "denormal_test",
    size = "small",
    srcs = ["denormal_test.cc"],
    deps = [
        ":denormal",
        ":test",
        ":test_main",
    ],
)

cc_library(
    name = "env",
    textual_hdrs = [
        "env.h",
        "file_system.h",
        "file_system_helper.h",
        "threadpool.h",
    ],
    deps = tf_windows_aware_platform_deps("env"),
)

cc_library(
    name = "env_impl",
    deps = tf_windows_aware_platform_deps("env_impl"),
)

cc_library(
    name = "env_time",
    compatible_with = get_compatible_with_portable(),
    textual_hdrs = ["env_time.h"],
    deps = tf_windows_aware_platform_deps("env_time"),
)

cc_library(
    name = "errors",
    srcs = ["errors.cc"],
    hdrs = ["errors.h"],
    deps = [
        ":logging",
        ":macros",
        ":platform",
        ":status",
        ":str_util",
        ":strcat",
        ":types",
        "@com_google_absl//absl/base:core_headers",
        "@com_google_absl//absl/strings",
    ],
)

cc_library(
    name = "dynamic_annotations",
    hdrs = ["dynamic_annotations.h"],
    compatible_with = get_compatible_with_portable(),
    deps = [
        ":platform",
    ] + tf_platform_deps("dynamic_annotations"),
)

cc_library(
    name = "gif",
    hdrs = ["gif.h"],
    deps = [
        "@gif",
    ],
)

cc_library(
    name = "mutex",
    compatible_with = get_compatible_with_portable(),
    textual_hdrs = ["mutex.h"],
    deps = tf_platform_deps("mutex"),
)

cc_library(
    name = "numbers",
    srcs = ["numbers.cc"],
    hdrs = ["numbers.h"],
    deps = [
        ":logging",
        ":macros",
        ":str_util",
        ":stringpiece",
        ":stringprintf",
        ":types",
        "@double_conversion//:double-conversion",
    ],
)

cc_library(
    name = "path",
    srcs = ["path.cc"],
    hdrs = ["path.h"],
    deps = [
        ":logging",
        ":mutex",
        ":scanner",
        ":strcat",
        ":stringpiece",
        ":types",
        "@com_google_absl//absl/algorithm:container",
    ],
    alwayslink = True,
)

cc_library(
    name = "protobuf",
    srcs = [
        "protobuf.cc",
        "protobuf_util.cc",
    ],
    hdrs = ["protobuf.h"],
    deps = [
        ":platform",
        ":types",
    ] + tf_protobuf_deps(),
)

cc_library(
    name = "regexp",
    hdrs = ["regexp.h"],
    deps = [
        ":platform",
        "@com_googlesource_code_re2//:re2",
    ],
)

cc_library(
    name = "resource",
    textual_hdrs = ["resource.h"],
    deps = [
        ":stringpiece",
    ] + tf_resource_deps(),
)

cc_library(
    name = "stack_frame",
    hdrs = ["stack_frame.h"],
    compatible_with = get_compatible_with_portable(),
)

cc_library(
    name = "status",
    srcs = ["status.cc"],
    hdrs = ["status.h"],
    deps = [
        ":logging",
        ":macros",
        ":mutex",
        ":stack_frame",
        ":stacktrace",
        ":str_util",
        ":strcat",
        ":stringprintf",
        ":types",
        "//tensorflow/core/protobuf:error_codes_proto_impl_cc",
        "//tensorflow/core/protobuf:for_core_protos_cc",
        "@com_google_absl//absl/base",
        "@com_google_absl//absl/status",
        "@com_google_absl//absl/strings",
        "@com_google_absl//absl/strings:cord",
        "@com_google_absl//absl/types:optional",
    ],
)

cc_library(
    name = "status_matchers",
    testonly = 1,
    srcs = ["status_matchers.cc"],
    hdrs = ["status_matchers.h"],
    deps = [
        ":status",
        ":statusor",
        ":test",
        "//tensorflow/core:protos_all_cc",
    ],
)

cc_library(
    name = "statusor",
    srcs = [
        "statusor.cc",
        "statusor_internals.h",
    ],
    hdrs = ["statusor.h"],
    deps = [
        ":errors",
        ":logging",
        ":macros",
        ":status",
        "//tensorflow/core/lib/core:errors",
        "@com_google_absl//absl/base:core_headers",
        "@com_google_absl//absl/strings",
        "@com_google_absl//absl/strings:str_format",
        "@com_google_absl//absl/types:span",
    ],
)

cc_library(
    name = "thread_annotations",
    hdrs = ["thread_annotations.h"],
    compatible_with = get_compatible_with_portable(),
)

cc_library(
    name = "test",
    testonly = True,
    compatible_with = get_compatible_with_portable(),
    textual_hdrs = ["test.h"],
    deps = tf_testing_deps("test") + [
        ":macros",
        ":platform",
        "@com_google_googletest//:gtest",
        "//tensorflow/core:tflite_portable_logging",
    ],
)

cc_library(
    name = "test_benchmark",
    testonly = True,
    hdrs = ["test_benchmark.h"],
    compatible_with = get_compatible_with_portable(),
    deps = [
        ":platform",
        "@com_google_benchmark//:benchmark",
    ],
)

filegroup(
    name = "test_hdrs",
    testonly = 1,
    srcs = [
        "test.h",
        "test_benchmark.h",
    ],
    compatible_with = get_compatible_with_portable(),
    visibility = [
        "//tensorflow/core:__pkg__",
        "//tensorflow/core/platform:__pkg__",
    ],
)

filegroup(
    name = "android_test_srcs",
    testonly = 1,
    srcs = [
        "test.h",
    ],
    compatible_with = get_compatible_with_portable(),
    visibility = [
        "//tensorflow/core:__pkg__",
        "//tensorflow/core/platform:__pkg__",
    ],
)

cc_library(
    name = "tracing",
    textual_hdrs = ["tracing.h"],
    deps = tf_platform_deps("tracing"),
)

cc_library(
    name = "tstring",
    hdrs = [
        "ctstring.h",
        "ctstring_internal.h",
        "tstring.h",
    ],
    compatible_with = get_compatible_with_portable(),
    deps = [
        ":cord",
        ":stringpiece",
    ],
)

filegroup(
    name = "ctstring",
    srcs = [
        "ctstring.h",
        "ctstring_internal.h",
    ],
    compatible_with = get_compatible_with_portable(),
)

filegroup(
    name = "lib_hdrs",
    srcs = [
        "bfloat16.h",
        "casts.h",
        "coding.h",
        "cpu_info.h",
        "crash_analysis.h",
        "dynamic_annotations.h",
        "env.h",
        "errors.h",
        "file_statistics.h",
        "file_system.h",
        "file_system_helper.h",
        "fingerprint.h",
        "init_main.h",
        "logger.h",
        "mem.h",
        "net.h",
        "numa.h",
        "path.h",
        "prefetch.h",
        "protobuf.h",
        "ram_file_system.h",
        "random.h",
        "resource.h",
        "stack_frame.h",
        "stacktrace.h",
        "stacktrace_handler.h",
        "statusor.h",
        "str_util.h",
        "strcat.h",
        "stringpiece.h",
        "stringprintf.h",
        "subprocess.h",
        "thread_annotations.h",
        "//tensorflow/tsl/platform/profile_utils:android_armv7a_cpu_utils_helper.h",
        "//tensorflow/tsl/platform/profile_utils:clock_cycle_profiler.h",
        "//tensorflow/tsl/platform/profile_utils:cpu_utils.h",
        "//tensorflow/tsl/platform/profile_utils:i_cpu_utils_helper.h",
    ],
    compatible_with = get_compatible_with_portable(),
)

# Header files for tensorflow/core:platform_base.
filegroup(
    name = "base_hdrs",
    srcs = [
        "byte_order.h",
        "env_time.h",
        "macros.h",
        "threadpool.h",
        "threadpool_interface.h",
    ],
    compatible_with = get_compatible_with_portable(),
)

filegroup(
    name = "framework_lite_hdrs",
    srcs = [
        "bfloat16.h",
        "byte_order.h",
        "cpu_info.h",
        "dynamic_annotations.h",
        "macros.h",
        "platform.h",
        "prefetch.h",
        "protobuf.h",
        "thread_annotations.h",
    ],
    compatible_with = get_compatible_with_portable(),
)

# Export source files needed for mobile builds, which do not use granular targets.
filegroup(
    name = "mobile_srcs_no_runtime",
    srcs = [
        "base64.cc",
        "base64.h",
        "bfloat16.h",
        "blocking_counter.h",
        "byte_order.h",
        "casts.h",
        "coding.cc",
        "coding.h",
        "cpu_info.cc",
        "cpu_info.h",
        "demangle.h",
        "denormal.cc",
        "denormal.h",
        "dynamic_annotations.h",
        "env.cc",
        "env.h",
        "env_time.h",
        "errors.cc",
        "errors.h",
        "file_statistics.h",
        "file_system.cc",
        "file_system.h",
        "file_system_helper.h",
        "hash.cc",
        "hash.h",
        "host_info.h",
        "init_main.h",
        "intrusive_ptr.h",
        "macros.h",
        "mem.h",
        "numa.h",
        "numbers.cc",
        "numbers.h",
        "path.cc",
        "path.h",
        "platform.h",
        "platform_strings_computed.h",
        "prefetch.h",
        "protobuf.cc",
        "protobuf.h",
        "protobuf_util.cc",
        "ram_file_system.h",
        "raw_coding.h",
        "regexp.h",
        "resource.h",
        "scanner.cc",
        "scanner.h",
        "setround.cc",
        "setround.h",
        "snappy.h",
        "stacktrace.h",
        "status.cc",
        "status.h",
        "statusor.cc",
        "statusor.h",
        "statusor_internals.h",
        "str_util.cc",
        "str_util.h",
        "strcat.cc",
        "strcat.h",
        "stringpiece.h",
        "stringprintf.cc",
        "stringprintf.h",
        "thread_annotations.h",
        "threadpool.h",
        "threadpool_interface.h",
        "tracing.h",
    ] + selects.with_or({
        "//tensorflow:fuchsia": tf_google_mobile_srcs_no_runtime(),
        "//conditions:default": [
            "//tensorflow/tsl/platform/default:mobile_srcs_no_runtime",
            "file_system_helper.cc",
            "threadpool.cc",
            "tracing.cc",
        ],
    }),
    compatible_with = get_compatible_with_portable(),
)

filegroup(
    name = "mobile_srcs_only_runtime",
    srcs = [
        "fingerprint.h",
        "random.cc",
        "random.h",
        "subprocess.h",
        "test_benchmark.h",
        "//tensorflow/tsl/platform/profile_utils:android_armv7a_cpu_utils_helper.cc",
        "//tensorflow/tsl/platform/profile_utils:android_armv7a_cpu_utils_helper.h",
        "//tensorflow/tsl/platform/profile_utils:cpu_utils.cc",
        "//tensorflow/tsl/platform/profile_utils:cpu_utils.h",
        "//tensorflow/tsl/platform/profile_utils:i_cpu_utils_helper.h",
    ],
    compatible_with = get_compatible_with_portable(),
    visibility = [
        "//tensorflow/core:__pkg__",
        "//tensorflow/core/platform:__pkg__",
    ],
)

filegroup(
    name = "gif_hdrs",
    srcs = [
        "gif.h",
    ],
    compatible_with = get_compatible_with_portable(),
    visibility = [
        "//tensorflow/core/lib/gif:__pkg__",
        "//tensorflow/core/platform:__pkg__",
    ],
)

filegroup(
    name = "legacy_lib_internal_headers",
    srcs = glob(
        [
            "*.h",
        ],
        exclude = [
            "dynamic_annotations.h",
            "gif.h",
            "jpeg.h",
        ],
    ) + [
        "//tensorflow/tsl/platform/profile_utils:android_armv7a_cpu_utils_helper.h",
        "//tensorflow/tsl/platform/profile_utils:cpu_utils.h",
        "//tensorflow/tsl/platform/profile_utils:i_cpu_utils_helper.h",
        "//tensorflow/tsl/platform/profile_utils:clock_cycle_profiler.h",
    ],
    compatible_with = get_compatible_with_portable(),
)

exports_files(
    [
        "host_info.h",
        "human_readable_json.h",
        "bfloat16.h",
        "cpu_info.h",
        "cpu_info.cc",
        "crash_analysis.h",
        "cuda_libdevice_path.h",
        "demangle.h",
        "env.cc",
        "env.h",
        "env_time.h",
        "file_system.cc",
        "file_system.h",
        "file_system_helper.cc",
        "file_system_helper.h",
        "init_main.h",
        "logging.h",
        "mem.h",
        "net.h",
        "numa.h",
        "ram_file_system.h",
        "resource_loader.h",
        "resource.h",
        "snappy.h",
        "stacktrace_handler.h",
        "cuda_libdevice_path.h",
        "test.h",
        "bfloat16.h",
        "logging.h",
        "rocm_rocdl_path.h",
        "subprocess.h",
        "threadpool.cc",
        "threadpool.h",
        "tracing.h",
        "tracing.cc",
    ],
    visibility = ["//tensorflow:__subpackages__"],
)

filegroup(
    name = "lib_proto_parsing_hdrs",
    srcs = [
        "init_main.h",
        "macros.h",
        "platform.h",
        "protobuf.h",
        "stringpiece.h",
    ],
    compatible_with = get_compatible_with_portable(),
    visibility = [
        "//tensorflow/core:__pkg__",
    ],
)

cc_library(
    name = "intrusive_ptr",
    hdrs = ["intrusive_ptr.h"],
    deps = [],
)

filegroup(
    name = "lib_internal_public_hdrs",
    srcs = [
        "blocking_counter.h",
        "demangle.h",
        "denormal.h",
        "host_info.h",
        "intrusive_ptr.h",
        "platform.h",
        "setround.h",
        "snappy.h",
        "tracing.h",
    ],
    compatible_with = get_compatible_with_portable(),
    visibility = [
        "//tensorflow/core:__pkg__",
        "//tensorflow/core/platform:__pkg__",
    ],
)

filegroup(
    name = "jpeg_hdrs",
    srcs = [
        "jpeg.h",
    ],
    compatible_with = get_compatible_with_portable(),
    visibility = [
        "//tensorflow/core:__pkg__",
        "//tensorflow/core/lib/jpeg:__pkg__",
    ],
)

cc_library(
    name = "jpeg",
    hdrs = ["jpeg.h"],
    deps = [
        "@libjpeg_turbo//:jpeg",
    ],
)

filegroup(
    name = "tflite_portable_logging_hdrs",
    srcs = [
        "bfloat16.h",
        "macros.h",
        "platform.h",
    ],
    compatible_with = get_compatible_with_portable(),
    visibility = [
        "//tensorflow/core:__pkg__",
        "//tensorflow/core/lib/jpeg:__pkg__",
    ],
)

filegroup(
    name = "jpeg_internal_hdrs",
    srcs = [
        "bfloat16.h",
        "dynamic_annotations.h",
        "macros.h",
        "mem.h",
        "platform.h",
        "stringpiece.h",
    ],
    compatible_with = get_compatible_with_portable(),
    visibility = [
        "//tensorflow/core:__pkg__",
        "//tensorflow/core/lib/jpeg:__pkg__",
        "//tensorflow/core/platform:__pkg__",
    ],
)

filegroup(
    name = "gif_internal_hdrs",
    srcs = [
        "bfloat16.h",
        "dynamic_annotations.h",
        "macros.h",
        "mem.h",
        "platform.h",
    ],
    compatible_with = get_compatible_with_portable(),
    visibility = [
        "//tensorflow/core:__pkg__",
        "//tensorflow/core/lib/gif:__pkg__",
        "//tensorflow/core/platform:__pkg__",
    ],
)

cc_library(
    name = "macros",
    hdrs = ["macros.h"],
    compatible_with = get_compatible_with_portable(),
)

filegroup(
    name = "xla_cpu_runtime_srcs",
    srcs = [
        "dynamic_annotations.h",
        "env_time.h",
        "macros.h",
        "platform.h",
    ],
    compatible_with = get_compatible_with_portable(),
)

cc_library(
    name = "net",
    textual_hdrs = ["net.h"],
    deps = tf_windows_aware_platform_deps("net"),
)

cc_library(
    name = "platform",
    hdrs = ["platform.h"],
    compatible_with = get_compatible_with_portable(),
)

cc_library(
    name = "platform_port",
    compatible_with = get_compatible_with_portable(),
    textual_hdrs = [
        "cpu_info.h",
        "demangle.h",
        "host_info.h",
        "init_main.h",
        "mem.h",
        "numa.h",
        "snappy.h",
    ],
    deps = tf_windows_aware_platform_deps("platform_port"),
)

cc_library(
    name = "platform_strings",
    srcs = [
        "platform_strings_computed.h",
    ],
)

cc_library(
    name = "protobuf_compiler",
    hdrs = ["protobuf_compiler.h"],
    deps = tf_protobuf_compiler_deps(),
)

cc_library(
    name = "random",
    srcs = ["random.cc"],
    hdrs = ["random.h"],
    deps = [
        ":mutex",
        ":types",
    ],
)

cc_library(
    name = "resource_loader",
    testonly = 1,
    textual_hdrs = ["resource_loader.h"],
    deps = tf_testing_deps("resource_loader"),
)

cc_library(
    name = "rocm_rocdl_path",
    textual_hdrs = ["rocm_rocdl_path.h"],
    deps = tf_platform_deps("rocm_rocdl_path"),
)

filegroup(
    name = "stacktrace_handler_hdrs",
    srcs = [
        "stacktrace_handler.h",
    ],
    compatible_with = get_compatible_with_portable(),
)

cc_library(
    name = "stacktrace_handler",
    textual_hdrs = ["stacktrace_handler.h"],
    deps = tf_windows_aware_platform_deps("stacktrace_handler"),
    alwayslink = 1,
)

cc_library(
    name = "str_util",
    srcs = ["str_util.cc"],
    hdrs = ["str_util.h"],
    deps = [
        ":logging",
        ":macros",
        ":stringpiece",
        ":types",
        "@com_google_absl//absl/strings",
    ],
)

cc_library(
    name = "strcat",
    srcs = ["strcat.cc"],
    hdrs = ["strcat.h"],
    deps = [
        ":logging",
        ":macros",
        ":numbers",
        ":stringpiece",
        ":types",
        "@com_google_absl//absl/meta:type_traits",
    ],
)

cc_library(
    name = "stringpiece",
    hdrs = ["stringpiece.h"],
    compatible_with = get_compatible_with_portable(),
    deps = [
        "@com_google_absl//absl/strings",
    ],
)

cc_library(
    name = "crash_analysis",
    hdrs = ["crash_analysis.h"],
    compatible_with = get_compatible_with_portable(),
    deps = [
        ":platform",
    ] + tf_platform_deps("crash_analysis"),
)

cc_library(
    name = "stringprintf",
    srcs = ["stringprintf.cc"],
    hdrs = ["stringprintf.h"],
    deps = [
        ":macros",
        ":types",
    ],
)

cc_library(
    name = "subprocess",
    textual_hdrs = [
        "subprocess.h",
    ],
    deps = tf_windows_aware_platform_deps("subprocess"),
)

cc_library(
    name = "cord",
    hdrs = ["cord.h"],
    compatible_with = get_compatible_with_portable(),
    deps = [
        ":platform",
        "@com_google_absl//absl/strings:cord",
    ] + tf_platform_deps("cord"),
)

cc_library(
    name = "threadpool_interface",
    hdrs = ["threadpool_interface.h"],
    compatible_with = get_compatible_with_portable(),
    deps = [
        ":mutex",
        ":types",
        "//third_party/eigen3",
        # TODO(ddunleavy) below needed for Eigen. Update once TSL is moved
        "//tensorflow/core/platform:mutex",
    ],
)

cc_library(
    name = "types",
    hdrs = ["types.h"],
    compatible_with = get_compatible_with_portable(),
    deps = [
        ":platform",
        ":bfloat16",
        ":tstring",
    ] + tf_platform_deps("types"),
)

cc_library(
    name = "build_test",
    testonly = 1,
    visibility = [
        "//tensorflow/core/platform:__pkg__",
    ],
    deps = [
        ":byte_order",
        ":fingerprint",
        ":gif",
        ":jpeg",
        ":macros",
        ":net",
        ":platform",
        ":platform_port",
        ":platform_strings",
        ":stacktrace_handler",
        ":stringpiece",
        ":threadpool_interface",
    ],
)

cc_library(
    name = "bfloat16",
    hdrs = ["bfloat16.h"],
    compatible_with = get_compatible_with_portable(),
    deps = [
        ":byte_order",
        "//third_party/eigen3",
    ],
)

cc_library(
    name = "logger",
    srcs = ["logger.cc"],
    hdrs = ["logger.h"],
    deps = [
        ":logging",
        ":protobuf",
        "//tensorflow/core/platform:env",
        "@com_google_absl//absl/base",
        "@com_google_absl//absl/synchronization",
    ],
    alwayslink = 1,
)

cc_library(
    name = "logging",
    compatible_with = get_compatible_with_portable(),
    textual_hdrs = ["logging.h"],
    visibility = [
        "//visibility:public",
    ],
    deps = tf_logging_deps(),
)

cc_library(
    name = "prefetch",
    hdrs = ["prefetch.h"],
    compatible_with = get_compatible_with_portable(),
    deps = [
        ":platform",
    ],
)

cc_library(
    name = "hash",
    srcs = ["hash.cc"],
    hdrs = ["hash.h"],
    compatible_with = get_compatible_with_portable(),
    deps = [
        ":macros",
        ":raw_coding",
        ":stringpiece",
        ":types",
    ],
)

cc_library(
    name = "human_readable_json",
    textual_hdrs = ["human_readable_json.h"],
    deps = tf_platform_deps("human_readable_json"),
)

cc_library(
    name = "raw_coding",
    hdrs = ["raw_coding.h"],
    compatible_with = get_compatible_with_portable(),
    deps = [
        ":byte_order",
        ":types",
    ],
)

filegroup(
    name = "lib_internal_private_hdrs",
    srcs = [
        "bfloat16.h",
        "raw_coding.h",
        "scanner.h",
        "str_util.h",
    ],
    compatible_with = get_compatible_with_portable(),
    visibility = ["//tensorflow/core:__pkg__"],
)

cc_library(
    name = "casts",
    hdrs = ["casts.h"],
    deps = [
        ":platform",
    ] + tf_platform_deps("casts"),
)

cc_library(
    name = "setround",
    srcs = ["setround.cc"],
    hdrs = ["setround.h"],
    deps = [
        ":logging",
        ":macros",
    ],
)

cc_library(
    name = "stacktrace",
    hdrs = ["stacktrace.h"],
    compatible_with = get_compatible_with_portable(),
    deps = [
        ":platform",
    ] + tf_windows_aware_platform_deps("stacktrace"),
)

cc_library(
    name = "cuda_libdevice_path",
    compatible_with = get_compatible_with_portable(),
    textual_hdrs = ["cuda_libdevice_path.h"],
    deps = tf_cuda_libdevice_path_deps(),
)

cc_library(
    name = "file_statistics",
    hdrs = ["file_statistics.h"],
    deps = [
        ":types",
    ],
)

cc_library(
    name = "fingerprint",
    hdrs = ["fingerprint.h"],
    compatible_with = get_compatible_with_portable(),
    deps = [
        ":stringpiece",
        ":types",
    ] + tf_fingerprint_deps(),
)

tf_cc_test(
    name = "fingerprint_test",
    size = "small",
    srcs = ["fingerprint_test.cc"],
    deps = [
        ":fingerprint",
        ":test",
        ":test_main",
        ":types",
    ],
)

cc_library(
    name = "cuda",
    hdrs = ["cuda.h"],
    deps = [
        ":platform",
        "//tensorflow/compiler/xla/stream_executor/cuda:cuda_activation_header",
    ],
)

tf_cuda_library(
    name = "stream_executor",
    srcs = ["stream_executor.h"],
    hdrs = [
        "cuda.h",
    ],
    features = ["-parse_headers"],
    deps = [
        "//tensorflow/tsl/platform/default/build_config:stream_executor",
    ],
)

cc_library(
    name = "tensor_float_32_utils",
    srcs = ["tensor_float_32_utils.cc"],
    hdrs = ["tensor_float_32_utils.h"],
    copts = tf_copts(),
    alwayslink = 1,
)

cc_library(
    name = "scanner",
    srcs = ["scanner.cc"],
    hdrs = ["scanner.h"],
    deps = [
        ":macros",
        ":str_util",
        ":stringpiece",
    ],
)

filegroup(
    name = "tensor_float_32_hdr",
    srcs = ["tensor_float_32_utils.h"],
    compatible_with = get_compatible_with_portable(),
)

cc_library(
    name = "tensor_float_32_hdr_lib",
    hdrs = [":tensor_float_32_hdr"],
    compatible_with = get_compatible_with_portable(),
)

tf_cc_test(
    name = "ctstring_test",
    size = "small",
    srcs = ["ctstring_test.cc"],
    deps = [
        ":tstring",
        "//tensorflow/core:test",
        "//tensorflow/core:test_main",
    ],
)

tf_cc_test(
    name = "hash_test",
    size = "small",
    srcs = ["hash_test.cc"],
    deps = [
        ":hash",
        ":logging",
        ":test",
        ":test_benchmark",
        "//tensorflow/core:test_main",
    ],
)

tf_cc_test(
    name = "tstring_test",
    size = "small",
    srcs = ["tstring_test.cc"],
    deps = [
        ":cord",
        ":stringpiece",
        ":tstring",
        "//tensorflow/core:test",
        "//tensorflow/core:test_main",
    ],
)

cc_library(
    name = "test_main",
    testonly = 1,
    srcs = ["test_main.cc"],
    copts = tf_copts(),
    linkopts = select({
        "//tensorflow:windows": [],
        "//conditions:default": ["-lm"],
    }),
    deps = [
        ":platform",
        ":stacktrace_handler",
        ":test",
        ":test_benchmark",
        "@com_google_absl//absl/strings",
        # TODO(ddunleavy) remove below once TSL has it's own test ruies
        "//tensorflow/core/platform:test",
    ],
    alwayslink = 1,
)
