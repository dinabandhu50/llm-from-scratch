## qLoRA - finding quantization levels

The information theoretically optimal data type for zero-mean normal distributions with 
arbitrary standard deviations σ in the range [−1, 1] is computed as follows: 
(1) estimate the 2^(k) + 1 quantiles of a theoretical N(0, 1) distribution to obtain a 
k-bit quantile quantization data type for normal distributions, 
(2) take this data type and normalize its values into the [−1, 1] range, 
(3) quantize an input weight tensor by normalizing it into the [−1, 1] range through 
absolute maximum rescaling. 

Once the weight range and data type range match, we can quantize as usual. Step (3) is 
equivalent to rescaling the standard deviation of the weight tensor to match the 
standard deviation of the k-bit data type. More formally, we estimate the 2^(k) values 
qi of the data type as follows:

$$ q_{i} = \frac{1}{2} * (Q_{X}(\frac{i}{2^{k} + 1}) + Q_{X}(\frac{i+1}{2^{k} + 1})) $$


A problem for a symmetric k-bit quantization is that this approach does not have an 
exact representation of zero, which is an important property to quantize padding and 
other zero-valued elements with no error. To ensure a discrete zeropoint of 0 and to 
use all 2^(k) bits for a k-bit datatype, we create an asymmetric data type by estimating 
the quantiles qi of two ranges qi:2^(k−1) for the negative part and 2^(k−1) + 1 for the 
positive part and then we unify these sets of qi and remove one of the two zeros that 
occurs in both sets. We term the resulting data type that has equal expected number of 
values in each quantization bin k-bit NormalFloat (NFk).