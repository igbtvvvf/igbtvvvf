using System;
using NAudio.Wave;

class Program
{
    static void Main()
    {
        string filePath = "path_to_accelerating_sound.wav";

        using (var audioFile = new AudioFileReader(filePath))
        using (var outputDevice = new WaveOutEvent())
        {
            outputDevice.Init(audioFile);
            outputDevice.Play();

            // Wait for the audio to finish playing
            while (outputDevice.PlaybackState == PlaybackState.Playing)
            {
                Console.WriteLine("Playing...");
                System.Threading.Thread.Sleep(500);
            }
        }

        Console.WriteLine("Playback finished.");
    }
}
