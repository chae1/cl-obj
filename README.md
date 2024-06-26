Common lisp macros for implicit struct accessing.
## Examples.
## defobj, defobjfun, objlet*, objdo*, defobjmacro, defobjmacrolet, etc.
Defining struct
```
(defstruct (obj (:conc-name nil))
  (head nil)
  (tail nil))
```
is equivalent to
```
(defobj obj!
  (head nil)
  (tail nil))
```
.\
Defining function
```
(defun compare-head (obj-1 obj-2)
  (if (< (head obj-1) (head obj-2))
      t
      nil))
```
is equivalent to
```
(defobjfun compare-head (obj!-1 obj!-2)
  (if (< head-1 head-2)
      t
      nil))
```
.\
let* binding
```
(let* ((obj1 (make-obj)))
  (setf (head obj1) 1))
```
is equivalent to
```
(objlet* ((obj!1 (make-obj!)))
  (setf head1 1))
```
.
## with-objs
```
(with-objs (obj!)
  nil)
```
is equivalent to
```
(objlet* ((obj!))
  nil)
```
.
```
(declaim (special obj!))
```
Define a function fn.
```
(with-objs (obj!)
  (defun fn ()
    (setf head 1)))
```
Call fn in the context where obj! is bound locally.
```
(objlet* ((obj! (make-obj!))
  (fn)))
```
fn will capture the variable obj! and set its head to 1.
