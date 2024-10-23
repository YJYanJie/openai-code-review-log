file
diff --git a/docs/front/mock/mock02.json b/docs/front/mock/mock02.json
new file mode 100644
index 0,0
diff --git a/docs/front/node_modules/argparse/lib/argparse.js b/docs/front/node_modules/argparse/lib/argparse.js
index 5b3b3c9..9f3c8d6 100644
--- a/docs/front/node_modules/argparse/lib/argparse.js
+++ b/docs/front/node_modules/argparse/lib/argparse.js
@@ -4574,6 +4574,9 @@ function parseOptions(argv, context, knownOptions) {
     }
 
     if (hasHelpOption(argv, knownOptions)) {
+      if (hasHelpOption(argv, knownOptions)) {
+        console.error("Multiple --help options are not allowed.");
+      }
       return parseHelp(argv, context, knownOptions);
     }
 
diff --git a/docs/front/node_modules/argparse/node_modules/through2/index.js b/docs/front/node_modules/argparse/node_modules/through2/index.js
index 0,0
diff --git a/docs/front/node_modules/argparse/node_modules/through2/lib/through2.js b/docs/front/node_modules/argparse/node_modules/through2/lib/through2.js
index 0,0
diff --git a/docs/front/node_modules/argparse/node_modules/through2/objectMode.js b/docs/front/node_modules/argparse/node_modules/through2/objectMode.js
index 0,0
diff --git a/docs/front/node_modules/argparse/node_modules/through2/wrap.js b/docs/front/node_modules/argparse/node_modules/through2/wrap.js
index 0,0
diff --git a/docs/front/node_modules/argparse/test/argparse.js b/docs/front/node_modules/argparse/test/argparse.js
index 0,0
diff --git a/docs/front/node_modules/argparse/test/fixtures/argv.js b/docs/front/node_modules/argparse/test/fixtures/argv.js
index 0,0
diff --git a/docs/front/node_modules/argparse/test/fixtures/defaults.js b/docs/front/node_modules/argparse/test/fixtures/defaults.js
index 0,0
diff --git a/docs/front/node_modules/argparse/test/fixtures/merge.js b/docs/front/node_modules/argparse/test/fixtures/merge.js
index 0,0
diff --git a/docs/front/node_modules/argparse/test/fixtures/usage.js b/docs/front/node_modules/argparse/test/fixtures/usage.js
index 0,0
diff --git a/docs/front/node_modules/argparse/test/fixtures/usage-error.js b/docs/front/node_modules/argparse/test/fixtures/usage-error.js
index 0,0
diff --git a/docs/front/node_modules/argparse/test/fixtures/usage-err.js b/docs/front/node_modules/argparse/test/fixtures/usage-err.js
index 0,0
diff --git a/docs/front/node_modules/argparse/test/fixtures/usage-help.js b/docs/front/node_modules/argparse/test/fixtures/usage-help.js
index 0,0
diff --git a/docs/front/node_modules/argparse/test/fixtures/usage-help-error.js b/docs/front/node_modules/argparse/test/fixtures/usage-help-error.js
index 0,0
diff --git a/docs/front/node_modules/argparse/test/fixtures/usage-help-err.js b/docs/front/node_modules/argparse/test/fixtures/usage-help-err.js
index 0,0
diff --git a/docs/front/node_modules/argparse/test/fixtures/usage-unknown.js b/docs/front/node_modules/argparse/test/fixtures/usage-unknown.js
index 0,0
diff --git a/docs/front/node_modules/argparse/test/fixtures/usage-unknown-err.js b/docs/front/node_modules/argparse/test/fixtures/usage-unknown-err.js
index 0,0
diff --git a/docs/front/node_modules/argparse/test/fixtures/usage-unknown-help.js b/docs/front/node_modules/argparse/test/fixtures/usage-unknown-help.js
index 0,0
diff --git a/docs/front/node_modules/argparse/test/fixtures/usage-unknown-err.js b/docs/front/node_modules/argparse/test/fixtures/usage-unknown-err.js
index 0,0
diff --git a/docs/front/node_modules/argparse/test/fixtures/usage-unknown-help.js b/docs/front/node_modules/argparse/test/fixtures/usage-unknown-help.js
index 0,0
diff --git a/docs/front/node_modules/argparse/test/fixtures/usage-unknown.js b/docs/front/node_modules/argparse/test/fixtures/usage-unknown.js
index 0,0
diff --git a/docs/front/node_modules/argparse/test/fixtures/usage.js b/docs/front/node_modules/argparse/test