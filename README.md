Forked from https://code.google.com/p/mp4parser/

This fork strips out a bunch of code and packages the remaining up as an Android Library.

The only way this library is being uses is to mux h264 streams into an MP4 container, so that is all that is expected to work.

There have been only slight modifications made to the original to get it working on android as a library.  You can see all those changes in the commit history.

Here is an example for usage to mux h264 into MP4.  

    try {
        H264TrackImpl h264Track = new H264TrackImpl( new BufferedInputStream( new FileInputStream( "/mnt/sdcard/encoded.h264" ) ) );
        Movie m = new Movie();
        m.addTrack( h264Track );
        IsoFile out = new DefaultMp4Builder().build( m );
        FileOutputStream fos = new FileOutputStream( new File( "/mnt/sdcard/encoded.mp4" ) );
        out.getBox( fos.getChannel() );
        fos.close();
    } catch ( IOException e ) {
        e.printStackTrace();
    }


Note android requires BufferedInputStream unlike the original example at https://code.google.com/p/mp4parser/source/browse/trunk/examples/src/main/java/com/googlecode/mp4parser/muxformats/H264Example.java