# Some Guidelines on Clojure Style

## General Style

Try to keep lines <= 80 columns long

## Declaring Functions

### Unless the entire function fits on one line, put the parameters vector on its own line

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
