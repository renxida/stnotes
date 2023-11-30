# To Run LLAMA with SHARK-Turbine

```bash
# make sure you have SHARK-Turbine cloned and set up

# if you don't use this specific version of brevitas, you will encounter `ModuleNotFoundError: No module named 'brevitas_examples.common'`
# during generate quantized safetensors
pip install -r turbine-models-requirement.txt

# generate vmfb with this:
python python/turbine_models/custom_models/stateless_llama.py --compile_to=vmfb --hf_model_name="llSourcell/medllama2_7b" --precision=f16 --quantization=int4  --external_weights=safetensors

# generate quantized safetensors via:
python python/turbine_models/gen_external_params/gen_external_params.py --hf_model_name="llSourcell/medllama2_7b" --precision=f16 --quantization=int4

# run vmfb vs torch model:
python python/turbine_models/custom_models/stateless_llama.py --run_vmfb --hf_model_name="llSourcell/medllama2_7b" --vmfb_path=medllama2_7b.vmfb --external_weight_file=medllama2_7b_f16_int4.safetensors 
```
(thanks Ian)

If you encounter `ModuleNotFoundError: No module named 'brevitas_examples.common'`, brevitas refactored `brevitas_examples.commmon` and you'll need an old version. Check turbin-models-requirements.txt or do `pip install brevitas @ git+https://github.com/Xilinx/brevitas.git@6695e8df7f6a2c7715b9ed69c4b78157376bb60b`

