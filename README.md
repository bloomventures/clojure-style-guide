# Some Guidelines on Clojure Style

## General Style

Try to keep lines <= 80 columns long

## Declaring Functions

### Unless the function is "trivial"¹, put the parameters vector on its own line

```clojure
; OKAY
(defn foo [x] (inc x))

; OKAY
(defn bar
  [{:keys [a b c]}]
  (println a b c))

; Pls don't
(defn quux [things]
  (for [thing things]
    (println thing)))
```

¹: Where "trivial" is deliberately left subjective

## Namespaces

Based on [How I NS](https://stuartsierra.com/2016/clojure-how-to-ns.html)

In summary, things should look like this:

```clojure
(ns com.example.my-application.server
  "Example application HTTP server and routing."
  (:refer-clojure :exclude [send])
  (:require
   [clojure.core.async :as async :refer [<! <!! >! >!!]]
   [com.example.my-application.base]
   [com.example.my-application.server.sse :as server.sse]
   [io.pedestal.http :as http]
   [io.pedestal.http.sse :as http.sse]
   [ring.util.response :as response])
  (:import
   (java.nio.file Files LinkOption)
   (org.apache.commons.io FileUtils)))
```

### Order of Elements in `ns` Form

Forms in the `ns` macro should be:
  1. `:refer-clojure` if any
  2. `:require` if any
  3. `:import` if any

### Sort imports and requires alphabetically

The `:require` and `:import` keywords should be followed by a newline, with all the following namespaces sorted alphabetically

### Always Wrap `require`'d namespaces in vectors

```clojure
; OKAY
(ns foo.stuff
  (:require
    [clojure.string :as string]
    [foo.things]))

; Pls don't
(ns foo.bloop
  (:require
    [clojure.string :as string]
    foo.things))
```

### Always wrap `import`'d packages in parenthesis

```clojure
; OKAY
(ns foo.blaap
  (:import
    (java.nio.file Files)))

; Pls don't
(ns foo.quupx
  (:import
    java.nio.file.Files)))
```
