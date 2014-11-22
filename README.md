freetype-simple
===============

Single line text rendering with [opengles](https://github.com/capsjac/opengles/) package available in Hackage.

Example
---------------

    import Graphics.OpenGLES
    import Graphics.Rendering.FreeType.Simple
    
    prepareTexture :: String -> GL (Texture R8)
    prepareTexture singleText = do
      font <- readFont "/usr/share/fonts/TTF/DejaVuSansMono.ttf"
      (bitmap, wh, bbox) <- textLine font 120.0 singleText
      glLoadTex2D Nothing True bitmap (fromIntegral <$> wh)

    draw :: GL ()
    draw = withGL $ do
      tex <- prepareTexture "The quick brown fox jumps over the lazy dog"
      setSampler tex (Sampler (clampToEdge,clampToEdge,Nothing) 16.0 (magLinear,minLinear))
      glDraw triangleStrip textShader
          [ texSlot 0 tex ] -- set the texture to slot 0
          [{- Uniform Variables -}]
          vao
          (takeFrom 0 4) -- make a billboard

LISENCE
---------------

Under Public Domain

Contact Information
-------------------

Contributions and bug reports are welcome!

