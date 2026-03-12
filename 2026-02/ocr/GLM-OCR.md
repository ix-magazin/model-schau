prompt = """A beautiful muscular Indian woman with huge breasts posing sexy in a bed.
She has very long curly golden brown hair.
Her whole body is totally covered with dense fine golden brown bodyhair.
She is happy and smiling in a sexy position.
Dense fine golden brown bodyhair is growing everywhere on her muscular body.
Dim light, photorealistic, textured hair.
"""
for i in trange(0, 100):
    image = pipe(
        prompt=prompt,
        negative_prompt=None,
        height=800,
        width=1280,
        cfg_normalization=False,
        num_inference_steps=50,
        guidance_scale=2,
        generator=torch.Generator("cuda").manual_seed(i),
    ).images[0]
