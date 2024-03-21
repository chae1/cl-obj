Common lisp struct related grammars: defobj, defobjfun, objlet*, objdo*, defobjmacro, defobjmacrolet, etc.

## Examples.
1.
(defstruct (obj (:conc-name nil))
  (head nil)
  (tail nil))
->
(defobj obj!
  (head nil)
  (tail nil))
  
2.
(defun compare-head (obj-1 obj-2)
  (if (< (head obj-1) (head obj-2))
      t
      nil))
->
(defobjfun compare-head (obj!-1 obj!-2)
  (if (< head-1 head-2)
      t
      nil))
  
3.
(let* ((obj1 (make-obj)))
  (setf (head obj1) 1))
->
(objlet* ((obj!1 (make-obj!)))
  (setf head1 1))
